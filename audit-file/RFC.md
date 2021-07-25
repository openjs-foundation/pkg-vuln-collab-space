# RFC: Audit decisions file format

**Authors**
- Zbigniew Tenerowicz - @naugtur


> The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## Definitions

- schema - see audit-file-schema.json
- package - NPM package 
- Audit File - file whose format is defined here.  *(I'm trying to avoid everyone getting distracted by discussing what the file name should be)*
- Advisory ID - NPM advisory ID. CVE numbers could be used as Advisory ID for greater interoperability. Existing implementations use NPM advisory ID.
- Maintainer - a maintainer (individual or organization) of a package
- Consumer - end-user application installing its dependencies. 

## Fields

- **owner** - When a package maintainer is publishing their decisions/recommendations, `owner.package` becomes resolution root for the paths in the dependency tree of a consumer when tooling attempts to apply/suggest the decisions from the Audit File. `owner` is optional, because it's unnecessary for end-user usecase. When publishing decisions, pakcage maintainers MUST add the `owner.package` field when providing their recommendations for the package users. Decision recommendations can be published without the scoping package, which means it's a set of general recommendations. 
- **decisions** - Keys in `decisions` MUST be a concatenation of the advisory id and the dependency path. Exact path, not just the name of the dependency, is a security requirement. In other words, a decision MUST refer to a specific installed instance of the vulnerable package. The path MUST NOT contain the `owner.package` as the beginning. A decision about a vulnerability reported against the `owner.package` 
Example key: `1179|nunjucks>chokidar>fsevents>node-pre-gyp>mkdirp>minimist`   

- **version** - Version of the file format/schema
- **rules** - A set of key-value props containing rules determining behavior of tooling forconsuming and producing the Audit File. (Keys for rules may be specified as this schema matures)

### Decisions

Meanings of various decisions:

|decision|by a Maintainer | by a Consumer |
| --- | --- | --- |
| `none` | explicitly no counter-claim <br> (report is valid, no fix) | N/A |
| `fix` | a fix was released and should be applied | a fix was applied <br>(tooling should warn on regression)|
| `ignore` + `expiresAt` | recommendation to temporarily ignore <br>(useful while work on impact verification is ongoing)| ignore temporarily <br>(various reasons)|
| `ignore` + `expiresAt: Infinity` | recommendation to permanently ignore <br>(not vulnerable, a counter-claim) | Ignore permanently|
| `postpone` | N/A | ignore for 24h <br>(a pressure vent to make CI green) |

Each decision can, and often should, be accompanied by `reason`. 

## Requirements for tooling
### Tools consuming Audit File

For better interoperability:
`HumanFriendlyDate` MUST allow unix timestamp. `HumanFriendlyDate` MUST allow YYYY-MM-DD to mean date in UTC. `HumanFriendlyDate` MUST allow ISODate


### Tools generating Audit File

A tool used to produce or edit the Audit File MUST format the JSON content to human readable form.


`HumanFriendlyDate` SHOULD be a simple human readable format with no timezone indication - YYYY-MM-DD.

## Usecases accounted for

- As a Maintainer I want to be able to verify and reject the claims made in an advisory / CVE
- As a Maintainer I want to be able to assert my package is not impacted by a vulnerable dependency
- As a Maintainer I don't want my assertion about no impact from a dependency cover the same package showing up elsewhere in my dependency tree when adopted by one of my other dependencies
- As a Maintainer I want to assert a fix exist in case my Consumer uses a registry proxy that is not up to date
- As a Maintainer I want to be able to recommend temporarily ignoring a vulnerability to my Connsumers when my research shows it's invalid but I'm still waiting for more details

- As a Consumer I want to track what has been fixed and avoid regression when someone on the team deletes lockfile
- As a Consumer I want the ability to temporarily ignore a vulnerability while I research it or while I wait for a fix to be released
- As a Consumer I want to permanently ignore vulnerabilities in areas of my dependencies I don't use
- As a Consumer I want to have an option to postpone dealing with the vulnerability till the next workday so I don't need to mark it as ignored
- As a Consumer I want the ability to temporarily ignore a vulnerability so I can build a security-conscious culture incrementally
- As a Consumer I want the Audit File to be human readable to serve as a history of decisions with attribution in git blame to serve as an audit trail.

- As a Consumer I want the ability to use Audit File from a Maintainer to get recommendations on decisons to make in the portion of my dependency tree starting at their package
- As a 3rd party advisor I want the ability to publish recommendations resulting from my research and backed by my reputation

## Open questions
 TBD
# preflight-demo-compromised

> **Controlled test case, historical incident.** This repository is not a real project. Its lockfile pins
> `@solana/web3.js` 1.95.6, one of the two versions published by an attacker in December 2024
> ([MAL-2024-11183](https://osv.dev/vulnerability/MAL-2024-11183),
> [GHSA-jcxm-7wvp-g6p5](https://osv.dev/vulnerability/GHSA-jcxm-7wvp-g6p5)). npm removed those versions, so this
> lockfile can't come from a real install today and can't be installed. **Do not try to install it.**

It demonstrates [dependency-preflight](https://github.com/lemind/dependency-preflight):

1. On `main`, the check reads `package-lock.json` and blocks: a known malicious version is locked.
2. A pull request upgrades to 1.95.8, the first fixed release. The check compares the pull request with `main` and
   comments: the malware finding is resolved, and the verdict moves from blocked to review (the 1.x line is still a
   major release behind `@solana/web3.js` 3.x).

## What the check does and does not do

It is an npm dependency assessment: it reads lockfiles and manifests and checks every locked version against public
advisory data (OSV). It is not a security audit: it doesn't read, build, test or run any code. The re-check on a pull
request compares dependency findings only; it is not an application test.

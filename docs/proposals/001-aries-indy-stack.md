# Aries Indy Stack

Strategy

 We propose behavior driven development for the initial approach. Describe behavior and add code in the [proposed](https://docs.google.com/drawings/d/1d-aCRC_Nzyywv9nyQif9_vBGbeWhp69M4T5_8_yYtAI/edit)[structure](https://docs.google.com/drawings/d/1sUffkRPlufingeeRjjBniVt9Ek3CNih9lUqym8mUl4M/edit). Demonstrate behavior, present code for review, and iterate on the proposed structure.

Aries will use [Did URIs to control resolver selection and pool selection](https://w3c-ccg.github.io/did-spec/#a-simple-example).

Development is starting in indy-node, working

Behavior

1. Context objects.
  - As a INDY user, I want to write a **context** (an object needed to support rich schemas) to the INDY ledger by specifying a did method and context so I can use them with rich schemas.
  - As a INDY user, I want to read a **context** from the INDY ledger by specifying a did so I can use it with rich schemas.
2. Fully resolvable Did&#39;s
  - As a INDY user, I would like to create a fully resolvable Did without knowledge of a ledger implementation.
  - As a INDY user, I want to use Aries to resolve my Did without knowledge of ledger implementation.
3. W3C Verifiable Credential
  - As a INDY user, I want to issue W3C compliant, verifiable credentials, so holders can present credential proofs.
4. W3C Verifiable Presentation
  - As a INDY user, I want to present a W3C verifiable credential to a verifier, so the verifier can confirm the authenticity of my credential.

Current development efforts.

- indy-node [https://github.com/ken-ebert/indy-node](https://github.com/ken-ebert/indy-node)
  - Context object read/write - DONE
  - Context object validation - under development
  - Context object unit test - under development
  - rs\_cred\_def object read/write - under development - adam  Flaming Wheels
  - rs\_Cred\_def object validation - open
  - rs\_Cred\_def object unit test - open
  - rs\_pres\_def read/write - under development - Flaming Wheels
  - rs\_pres\_def validation - open
  - rs\_pres\_def unit test - open
  - rs\_Encoding object read/write - under development - Flaming Wheels
  - rs\_Encoding object validation -
  - rs\_Encoding object unit test -
  - rs\_Mapping object read/write - under development - Flaming Wheels
  - rs\_Mapping object validation -
  - rs\_Mapping object unit test -
  - rs\_Schema object read/write - under development - Flaming Wheels
    * Schemas are stored in json\_ld &quot;expanded form&quot;. Provided context object will allow [compaction](https://www.w3.org/TR/json-ld-api/#dfn-compaction) or &quot;compact form&quot;.
  - rs\_Schema object validation -
  - rs\_Schema object unit test -
  - Replace indy-crypto with ursa - pending…
  - Removing indy-sdk dependancy - open
    * This could be done by hard code txn&#39;s with signatures in tests And extending the internal bus to allow raising txn messages, bypassing zmq
  - rs\_did\_doc object read/write- Flaming Wheels
  - rs\_did\_doc object - open
    * create a new W3C compliant did\_doc object
    * Include in authorization checks
    * Deprecate old object creation
      - This will restrict raw data being put on the ledger as attrib&#39;s.
- Indy-resolver [https://github.com/mikelodder7/indy-resolver](https://github.com/mikelodder7/indy-resolver)
  - Zmq ledger.
    * connect from gen/ connect from pool state,
    * Consensus
      - Persist **Patricia trie** and pool state in … (the wallet???).
    * Build\_txn,
    * sign\_txn,
    * send.
  - Implement Nym (did) API outlined [here](https://github.com/mikelodder7/indy-resolver/blob/master/libindyresolver/include/indy_resolver_did.h) using zmq methods from above.
- Aries-sdk [https://github.com/dbluhm/aries-sdk](https://github.com/dbluhm/aries-sdk)
  - Did creation using Ursa
  - Anon\_cred 2.0
    * Issue verifiable credentials (w3c compliant)
    * Verify credentials
- Aries-wallet [https://github.com/dbluhm/aries-sdk/blob/master/docs/split-ideas.md#optional-wallet](https://github.com/dbluhm/aries-sdk/blob/master/docs/split-ideas.md#optional-wallet)
  - Wallet design/redesign, encrypted?, postgres?...
    * Anon\_cred 2.0 introduces complex credentials that require complex DB queries to fulfill presentations, indy-sdk wallet may not handle this well…
  - Wrap Aries-sdk with a db persistence.
    * Store Did in the wallet.
- Aries-sdk-python [https://github.com/dbluhm/aries-sdk-python](https://github.com/dbluhm/aries-sdk-python)
  - Describe user API for did Scenarios (started)

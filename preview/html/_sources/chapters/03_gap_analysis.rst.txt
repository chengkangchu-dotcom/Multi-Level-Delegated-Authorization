.. raw:: latex

   \clearpage

Gap analysis
============

The comparison uses the three proposed requirements defined in Chapter 2: permission attenuation
(R1), agent identity and key binding (R2), and selective disclosure (R3). An illustrative two-level
delegation flow is provided in Annex A.

This preliminary analysis follows the two complementary formats in ITU-T A Suppl. 6, clause 7 and
Appendix I [P4]: an inventory of related work followed by identified gaps, proposed studies and
related activities. The comparison is limited to the cited editions and public proposals reviewed on
14 November 2026. The gaps concern interoperable composition of R1-R3 across trust domains; they do
not imply that the underlying mechanisms are unavailable or unstudied.

Existing standards and reusable mechanisms
------------------------------------------

+--------------------------------+--------------------------------+--------------------------------+
| Organization and reference     | Relevant coverage              | Remaining issue for this       |
|                                |                                | proposal                       |
+================================+================================+================================+
| IETF: OAuth 2.0 Token          | Token exchange supports        | Section 4.1 treats earlier     |
| Exchange, RFC 8693 [T1];       | delegation and actor           | actors as history, not         |
| Standards Track RFC            | identification. Nested actor   | access-control inputs. The RFC |
|                                | claims record previous actors. | does not define a              |
|                                |                                | verifier-checkable             |
|                                |                                | permission-subset proof at     |
|                                |                                | every delegation step or       |
|                                |                                | selective disclosure of parent |
|                                |                                | authority.                     |
+--------------------------------+--------------------------------+--------------------------------+
| IETF: OAuth Rich Authorization | Structured, fine-grained       | Section 6.1 leaves comparison  |
| Requests, RFC 9396 [T9];       | authorization details for      | rules to each authorization    |
| Standards Track RFC            | specific APIs and              | type. Providers need agreed    |
|                                | transactions.                  | semantics for deciding whether |
|                                |                                | a child grant is contained in  |
|                                |                                | its parent; JSON structure     |
|                                |                                | alone does not provide those   |
|                                |                                | rules.                         |
+--------------------------------+--------------------------------+--------------------------------+
| IETF: OAuth DPoP, RFC 9449     | Sender-constrained tokens and  | A DPoP key is not, by itself,  |
| [T2]; Standards Track RFC      | proof of key possession bind   | a trusted agent identity or    |
|                                | token use to an HTTP method    | authority to delegate. Section |
|                                | and URI.                       | 11.7 excludes general          |
|                                |                                | request-body integrity; the    |
|                                |                                | proposed profile also needs    |
|                                |                                | binding to relevant operation  |
|                                |                                | parameters and a delegation    |
|                                |                                | profile.                       |
+--------------------------------+--------------------------------+--------------------------------+
| IETF: SD-JWT, RFC 9901 [T3];   | Selective disclosure of signed | Selective disclosure does not  |
| Standards Track RFC            | claims, with an optional       | establish a child's authority  |
|                                | holder-key-binding mechanism.  | under its parent or prove      |
|                                |                                | inequalities over hidden       |
|                                |                                | limits. An authorization       |
|                                |                                | profile must require key       |
|                                |                                | binding and identify claims or |
|                                |                                | proofs essential to each       |
|                                |                                | decision, consistent with      |
|                                |                                | Section 9.7.                   |
+--------------------------------+--------------------------------+--------------------------------+
| W3C: Verifiable Credentials    | Common issuer, holder,         | Section 5.9 explicitly         |
| Data Model v2.0 [T5];          | verifier and credential data   | requires an accompanying       |
| Recommendation                 | model, usable with suitable    | authorization framework. The   |
|                                | securing mechanisms.           | data model alone does not      |
|                                |                                | define permission attenuation, |
|                                |                                | authorized re-delegation or an |
|                                |                                | agent-specific use proof.      |
+--------------------------------+--------------------------------+--------------------------------+

These standards provide complementary building blocks. The issue is their composition: exchanging a
token, proving a key and disclosing selected claims are separate operations. This proposal seeks
common rules connecting an accepted root grant to each child agent and to the verifier's decision
under R1-R3. It does not propose replacing OAuth or the VC data model.

Related drafts and FG-TIDA proposals
------------------------------------

+--------------------------------+--------------------------------+--------------------------------+
| Organization and reviewed work | Relevant coverage              | Remaining issue for this       |
|                                |                                | proposal                       |
+================================+================================+================================+
| IETF submission: Attenuating   | Local attenuation, a defined   | Section 10 acknowledges that   |
| Authorization Tokens, draft    | tool-constraint vocabulary,    | chains can reveal task, tool,  |
| -02 [T4]                       | holder-key binding and         | constraint and key-correlation |
|                                | invocation proof of            | information. Its               |
|                                | possession.                    | chain-validation mechanism     |
|                                |                                | does not provide task-branch   |
|                                |                                | selective disclosure with      |
|                                |                                | proof of inherited             |
|                                |                                | constraints.                   |
+--------------------------------+--------------------------------+--------------------------------+
| IETF submission: Verifiable    | Parent commitments,            | Verification uses the signed   |
| Attenuated Delegation for AI   | deterministic attenuation      | tokens in the chain. The       |
| Agent Chains, draft -03 [T7]   | checks, bounded depth and      | reviewed profile does not      |
|                                | expiry, principal continuity   | specify a selectively          |
|                                | and DPoP-based key possession. | disclosed parent-evidence      |
|                                |                                | representation that hides      |
|                                |                                | unrelated permissions while    |
|                                |                                | preserving those checks.       |
+--------------------------------+--------------------------------+--------------------------------+
| IETF submission: OAuth 2.0     | An authorization server issues | Section 11 identifies          |
| Delegated Authorization, draft | a key-bound root; clients      | information exposure when      |
| -04 [T8]                       | locally sign constrained child | resource servers receive the   |
|                                | tokens. The draft defines      | full chain. The reviewed       |
|                                | chain checks and type-specific | profile does not specify       |
|                                | permission containment.        | selectively disclosed parent   |
|                                |                                | evidence that preserves its    |
|                                |                                | chain and containment checks.  |
+--------------------------------+--------------------------------+--------------------------------+
| W3C: Data Integrity BBS        | Selective disclosure and       | Deriving a presentation does   |
| Cryptosuites v1.0 [T6];        | unlinkable derived proof       | not itself authorize a new     |
| Candidate Recommendation Draft | artifacts, including optional  | agent or prove parent-child    |
|                                | holder-binding features.       | policy containment. An         |
|                                |                                | authorization profile and, for |
|                                |                                | hidden numeric comparisons, an |
|                                |                                | additional compatible proof    |
|                                |                                | mechanism are needed.          |
+--------------------------------+--------------------------------+--------------------------------+
| FG-TIDA public themes: ATHENA, | Overlapping proposals address  | These theme descriptions do    |
| issue #34 [F1];                | constrained delegation, agent  | not specify the combined       |
| Subject-Anchored Identity,     | binding and cross-domain       | credential and disclosure      |
| Delegation and Discovery,      | verification; ATHENA also      | profile studied here. The      |
| issue #45 [F2]                 | addresses privacy.             | proposed work should           |
|                                |                                | contribute cross-domain        |
|                                |                                | delegation use cases and the   |
|                                |                                | R1-R3 analysis to these        |
|                                |                                | activities and identify        |
|                                |                                | opportunities to consolidate   |
|                                |                                | work.                          |
+--------------------------------+--------------------------------+--------------------------------+

The three Internet-Drafts are individual submissions and work in progress, not adopted IETF
standards. The W3C BBS document is a draft rather than a Recommendation; the FG-TIDA issues are
discussion proposals rather than approved ITU-T specifications. In particular, [T4], [T7] and [T8]
already specify attenuation and key binding. Their overlap narrows the justification for this work
to interoperable composition and privacy, rather than the invention of delegation itself.

Identified gaps and proposed studies
------------------------------------

GAP-01 - Common attenuation semantics across service domains
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Gap description.** R1 needs different providers to interpret the same action, resource, audience,
limit and delegation condition consistently. The reviewed drafts provide concrete containment rules
within their respective vocabularies; a shared mapping across heterogeneous service domains is not
established by those separate specifications. Hidden parent information must not make containment
undecidable or let an applicable restriction be omitted.

**Future work.** Compare and reuse existing vocabularies and containment rules, identify only the
missing mappings, and define how an implementation handles unsupported or undisclosed constraints.
Use a bounded set of cross-domain task types, with Annex A as one illustrative flow.

**Related work.** RFC 8693 [T1]; Rich Authorization Requests [T9]; the delegation drafts [T4], [T7],
[T8]; FG-TIDA themes [F1], [F2].

GAP-02 - Verifiable root authority linked to delegated agents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Gap description.** R2 requires each delegation to link authorized agents and their keys. Verifiers
also need a trusted basis for accepting root authority. Existing identity, key-possession and
delegation mechanisms cover substantial parts of this chain; their composition needs explicit rules
for root-authority trust, cross-domain identity mappings and operation binding, including when
parent evidence is selectively disclosed. A valid signature alone cannot establish the principal's
rights at a service.

**Future work.** Specify the roles and trust evidence needed to accept a root grant, bind each grant
to its designated agent, and bind execution to the intended operation. Reuse existing identity and
PoP mechanisms; treat the user-signed root in Annex A as one issuance model.

**Related work.** DPoP [T2]; VC Data Model [T5]; delegation drafts [T4], [T7], [T8]; FG-TIDA themes
[F1], [F2].

GAP-03 - Selective disclosure with verifiable attenuation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Gap description.** R3 requires an agent to receive only relevant authorization information while
the verifier still checks R1 and R2. The reviewed delegation drafts expose parent token contents
needed for chain checks; SD-JWT and BBS provide disclosure mechanisms without defining delegated
authority. Simply combining their formats does not establish that hidden constraints were respected
or that a new recipient was authorized.

**Future work.** Study a delegation and presentation profile that hides unrelated task branches,
preserves authenticated evidence of all applicable constraints, and binds that evidence to the child
agent. Separately assess proofs over hidden parent values as an enhanced research objective. Compare
disclosure and correlation properties before selecting a construction.

**Related work.** SD-JWT [T3]; BBS Cryptosuites [T6]; delegation drafts [T4], [T7], [T8]; ATHENA
[F1].

These findings will inform the Technical Report described in Chapter 4, identifying reusable
mechanisms, missing capabilities and opportunities to coordinate with related FG-TIDA work. The
analysis does not select a credential format or claim that every gap requires a new standard.

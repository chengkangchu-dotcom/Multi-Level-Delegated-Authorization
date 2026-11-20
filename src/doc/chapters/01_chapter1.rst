Introduction
============

Problem statement
-----------------

AI agents may delegate parts of a task to other agents across service providers and trust domains.
Capability discovery and ecosystem connectivity determine which agents can perform each subtask.
Knowing that an agent offers a function does not establish that it may exercise authority on behalf
of a user or organization.

Forwarding a broad bearer credential to every downstream agent exposes unnecessary permissions and
creates opportunities for credential reuse. Forwarding the complete authorization plan also reveals
unrelated tasks, service relationships and sensitive constraints. Requiring fresh approval for every
downstream step can undermine useful autonomous execution.

The proposed outcome is a verifiable way to distribute only the authority needed for each subtask,
within the boundaries set by an authorizing principal. Each agent must act under its own identity
and key, without impersonating that principal or reusing another agent's private key.

Scope and initial boundaries
----------------------------

The work covers root authorization, explicit permission to delegate, child grant derivation, agent
identity and key binding, downstream verification, selective disclosure, and gaps in combining these
capabilities. The authorizing principal may be a user or organization; root approval and issuance
depend on the deployment and the verifier's trust policy. Annex A illustrates two delegation edges
using a user-signed root. The model should generalize to a bounded number of levels.

The work is independent of an operating system, vendor, credential format or identifier scheme.
Agents may run on devices, enterprise systems or cloud platforms. DID-based identifiers,
certificates and other trusted identity-to-key bindings can be evaluated. An identifier or
application name alone is insufficient authentication.

The proposed deliverable is a Technical Report on use cases, requirements, a reference model and
gaps. It does not define a production-ready protocol, mandate a ledger, or replace service access
policies. Key protection, approval interfaces where applicable and optional runtime attestation
support authorization verification.

Requested Incubation action
---------------------------

The proposer requests that Incubation consider this topic, invite collaborators and determine its
relationship to existing trust, identity and authorization work. If accepted, the group should
assign an appropriate organizational home and develop the Technical Report in Chapter 4 through the
FG-TIDA process [P1]. This proposal does not presume adoption, a working-group assignment or an
official document number.

Terms used in this proposal
---------------------------

+-------------------------------------------------+-------------------------------------------------+
| Term                                            | Meaning                                         |
+=================================================+=================================================+
| Root grant G0                                   | Initial authorization established by an         |
|                                                 | authorizing principal and bound to agent A.     |
+-------------------------------------------------+-------------------------------------------------+
| Child grant G1                                  | Authorization issued or derived by A under G0   |
|                                                 | and bound to downstream agent B.                |
+-------------------------------------------------+-------------------------------------------------+
| Attenuation                                     | Reduction, or preservation without expansion,   |
|                                                 | of effective permissions and constraints.       |
+-------------------------------------------------+-------------------------------------------------+
| Proof of possession (PoP)                       | Evidence that the current actor controls the    |
|                                                 | private key bound to its authorization.         |
+-------------------------------------------------+-------------------------------------------------+
| Parent evidence                                 | Authenticated information or proofs needed to   |
|                                                 | verify the child's derivation and applicable    |
|                                                 | inherited constraints.                          |
+-------------------------------------------------+-------------------------------------------------+
| Two-level example                               | Two delegation edges: principal to A, then A to |
|                                                 | B; B may not delegate further in Annex A.       |
+-------------------------------------------------+-------------------------------------------------+

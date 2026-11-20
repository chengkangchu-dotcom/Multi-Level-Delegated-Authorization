.. raw:: latex

   \clearpage

Proposed requirements
=====================

.. raw:: latex

   \enlargethispage{1\baselineskip}
   \titlespacing*{\section}{0pt}{9pt}{4pt}

These are proposed requirements for discussion in Incubation. The word **shall** expresses a
requirement of the proposed design, not an already approved FG-TIDA requirement.

R1 - Monotonic permission attenuation
-------------------------------------

Every child grant shall authorize no more than its parent permits for that delegation. For an
operation x and resource/task context c, the intended invariant is:

   EnvelopeAllows(G_child, x, c) implies EnvelopeAllows(G_parent, x, c).

Here the permission envelope excludes the change of authorized holder from A to B. That identity
transition is verified separately under R2; it does not grant B the right to use A's parent
credential.

This implication covers actions, resources, service audiences, data categories, purposes, locations
where relevant, amounts, counts, time windows and delegation conditions. Validity intervals shall
remain within the parent's interval. Delegation shall be allowed explicitly and the remaining
permitted depth shall decrease at each delegation step.

The specification shall define deterministic interpretation of constraints, including resource
identifiers, currency and units, time boundaries and unsupported expressions. A verifier shall
reject unknown critical constraints, inconsistent meanings or a subset relationship that it cannot
establish. A child's narrower positive permissions shall not erase an inherited prohibition.

R2 - Binding authorization to agent identity
--------------------------------------------

Each grant shall bind its authorized agent to an authenticated identity and a specific public key or
equivalent verifiable key reference. Each child issuer shall be the authorized holder of the parent
grant and shall possess the parent's delegation authority.

The executing agent shall demonstrate possession of the corresponding private key. The proof shall
be bound to the presented authorization, verifier, fresh challenge or equivalent replay-resistant
context, and the operation with its security-relevant parameters. Any mapping to a concrete
transport shall specify exactly what is signed. DPoP is relevant prior work, but does not by itself
sign arbitrary application request bodies [T2].

Copying G1 to another agent shall not enable its use with that agent's key. Parent and child agents
shall use separate keys. Key rotation, compromise, revocation and re-binding rules shall not allow
silent transfer of authority. This property depends on protecting private keys; it does not prevent
a compromised authorized agent from misusing its own key.

R3 - Selective disclosure of authorization information
------------------------------------------------------

Delegation and presentation shall support withholding unrelated task branches, sibling permissions
and other information unnecessary for the recipient's operation. The verifier shall still obtain
authenticated evidence for all constraints that affect its authorization decision.

Two privacy objectives are distinguished:

1. **Required baseline:** disclose the selected task branch and all applicable global and branch
   constraints; hide unrelated branches. This supports cross-domain delegated workflows.
2. **Enhanced research objective:** hide selected applicable parent values, such as the parent's
   exact spending ceiling, while proving the child's compliance. Such a profile requires a suitable
   predicate, range or other verifiable proof mechanism.

Selective disclosure shall not make omitted constraints disappear. A profile shall define mandatory
disclosure or proof rules. A valid signature on a partially disclosed credential does not, by
itself, prove attenuation. Privacy claims shall specify the observer, disclosed information,
remaining correlation and any reliance on an online verifier.

.. raw:: latex

   \titlespacing*{\section}{0pt}{12pt}{6pt}

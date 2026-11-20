.. raw:: latex

   \titlespacing*{\section}{0pt}{4pt}{2pt}
   \small
   \pagestyle{plain}
   \thispagestyle{plain}
   \let\osiaorigaddcontentsline\addcontentsline
   \renewcommand{\addcontentsline}[3]{}

.. _chapter-overview:

.. only:: html

   .. admonition:: Proposer review draft

      Version 1.0. Prepared for Incubation consideration; not submitted or approved.

Multi-Level Delegated Authorization
===================================

.. raw:: latex

   \vspace*{-10pt}

**Incubation work item proposal \| Version 1.0 \| 20 November 2026**

**Status:** Prepared for proposer review. Not submitted, adopted or approved.

.. only:: html

   `Download this proposal as a PDF <specification.pdf>`_.

.. raw:: latex

   % Front-matter sections share the index page; restore chapter before the TOC.
   \let\osiafrontmatterchapter\chapter
   \let\chapter\section

.. Keep front matter in one block so the chapter toctrees below remain at
   document level, rather than becoming children of the final Note section.

.. only:: html or latex

   Abstract
   --------

   AI agents may delegate tasks across service providers and trust domains. This contribution proposes
   an Incubation work item combining monotonic permission attenuation, binding to the authorized
   agent's identity and key, and selective disclosure of authorization information.

   An authorizing principal establishes a root grant; each authorized agent may derive narrower grants
   for designated downstream agents. Verifiers check root authority, delegation evidence, proof of key
   possession and applicable constraints. A two-level user-authorized flow illustrates the model
   without prescribing a root-issuance mechanism. The proposed outcome is a Technical Report covering
   use cases, requirements, a reference model and gap analysis.

   Authors
   -------

   .. list-table::
      :header-rows: 1
      :widths: 22 34 44

      * - Name
        - Affiliation
        - Contact
      * - Cheng-Kang CHU
        - Huawei Technologies Co., Ltd
        - Chu.Cheng.Kang@huawei.com
      * - Tieyan LI
        - Huawei Technologies Co., Ltd
        - Li.tieyan@huawei.com
      * - Ye TAO
        - China Unicom
        - taoy10@chinaunicom.cn
      * - Ying WANG
        - China Unicom
        - wangy2173@chinaunicom.cn
      * - Liangliang ZHANG
        - Huawei Technologies Co., Ltd
        - Liangliang.zhang@huawei.com

   Keywords
   --------

   AI agents; multi-level delegation; permission attenuation; agent identity; proof of possession;
   selective disclosure; cross-domain authorization.

   Foreword
   --------

   This is a proposed contribution to the ITU-T Focus Group on Trust and Identity for Humans and
   Agentic AI (FG-TIDA), whose parent group is ITU-T Study Group 17 [P3]. It addresses how a
   principal's authority can be distributed across cooperating agents with verifiable boundaries and
   limited disclosure.

   The document is prepared from the FG-TIDA specification template [P2]. Its content is offered for
   Incubation discussion and does not represent an adopted position of the Focus Group, an ITU-T
   Recommendation or an approved standard.

   Note
   ----

   No official contribution identifier, working-group assignment or approval date has been assigned.
   The example flow and requirements are a starting point for study, not a complete implementation
   specification.

.. raw:: latex

   \let\chapter\osiafrontmatterchapter
   \let\addcontentsline\osiaorigaddcontentsline
   \titlespacing*{\section}{0pt}{12pt}{6pt}
   \normalsize
   \clearpage
   \sphinxtableofcontents
   \osiamainmatter

.. toctree::
   :maxdepth: 3
   :numbered:
   :hidden:

   chapters/01_introduction
   chapters/02_requirements
   chapters/03_gap_analysis
   chapters/04_deliverable
   chapters/05_references

.. toctree::
   :maxdepth: 3
   :hidden:

   chapters/annex_a

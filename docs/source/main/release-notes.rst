Release Notes
=============

**MythX API v1.4.1**

This release deploys a hotfix that fixes analysis scheduler crashes on server start-up.

**MythX API v1.4.0**

API v1.4.0 Introduces revised rate limits on requests, analysis queue and analysis workers running in
parallel for a given user.

This change breaks compatibility with older client libraries if they send too frequent polling requests. Update to `armlet v2.0.0 <https://github.com/ConsenSys/armlet>`_ or higher or follow the recommendations in :ref:`Rate Limits` to ensure compatility.


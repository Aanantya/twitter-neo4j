<!-- vscode-markdown-toc -->
* 1. [Vision](#Vision)
* 2. [Functional requirements](#Functionalrequirements)
* 3. [Non-functional requirements](#Non-functionalrequirements)
* 4. [Architecture](#Architecture)
* 5. [Use cases walkthrough](#Usecaseswalkthrough)
	* 5.1. [Below use-case talks about how the users are divided in buckets.](#Belowuse-casetalksabouthowtheusersaredividedinbuckets.)
	* 5.2. [Below use-case talks how multiple clients takes items and update. Also, it talks about challenges](#Belowuse-casetalkshowmultipleclientstakesitemsandupdate.Alsoittalksaboutchallenges)
	* 5.3. [Below use-case talks about error conditions which can happen in this system](#Belowuse-casetalksabouterrorconditionswhichcanhappeninthissystem)
	* 5.4. [Below use-case captures various software exceptions](#Belowuse-casecapturesvarioussoftwareexceptions)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
# DM check subsystem

##  1. <a name='Vision'></a>Vision
Multiple clients like to contribute in checking openDM. These clients can come and go anytime. System should provide fault tolerant and fast soltion for them to contribute.

## Requirements break-down
###  2. <a name='Functionalrequirements'></a>Functional requirements
* Multiple clients should be able to fetch user list for checking
* Only the client who got the user list should be able to update
* Only registered client should be able to interact with system
* In case of any difficulyt(Crash for example), Client should be able to recollect its owned user list with the help of system
* User should be able to give list of users which needs high priority for processing OpenDM
* User should be able to view list of users which are not yet marked for processing.

###  3. <a name='Non-functionalrequirements'></a>Non-functional requirements
* Clients should not wait for getting user list
* Client should not wait while updaing openDM info for user
* System should be fair to users for OpenDM check. It means that no user openDM check should be starved for ever
* System should unlock user lists owned by dead clients and reassigns
* System should have minimal load on DB while its processing
* System should have a resonable maximum wait time for processing any user openDM once it marked for processing. For non-marked, user, its fine as user can assing if needed.
* System should be able to scale with reasonable limit. Limit should be advertised


##  4. <a name='Architecture'></a>Architecture
This problem can be mapped to public distribution system(PDS). Note that PDS shops gives the fix amount of groceriers to multiple card holders. Card holder can be anyone who has government approval. Generally on distribution day, there will be queue. To speedize, this shop owner makes bucket of rations as pre-processing. This helps shop owner to distribute ration in parallel.

##  5. <a name='Usecaseswalkthrough'></a>Use cases walkthrough
###  5.1. <a name='Belowuse-casetalksabouthowtheusersaredividedinbuckets.'></a>Below use-case talks about how the users are divided in buckets.
![image info](./data/usecases_for_bucket_creation.jpg)

###  5.2. <a name='Belowuse-casetalkshowmultipleclientstakesitemsandupdate.Alsoittalksaboutchallenges'></a>Below use-case talks how multiple clients takes items and update. Also, it talks about challenges
![image info](./data/usecase_multi_client_processing.jpg)

###  5.3. <a name='Belowuse-casetalksabouterrorconditionswhichcanhappeninthissystem'></a>Below use-case talks about error conditions which can happen in this system
![image info](./data/usecase_error_Conditons_handling.jpg)

###  5.4. <a name='Belowuse-casecapturesvarioussoftwareexceptions'></a>Below use-case captures various software exceptions
![image info](./data/usecases_for_software_exceptions.jpg)

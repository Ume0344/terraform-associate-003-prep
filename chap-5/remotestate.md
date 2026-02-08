## Remote state
- statefiles shuld be stored in secure shared state backend. Why not to store it locally or on version control systems.
    - Creates inconsistencies.
    - Sensitive data might get revealed.
- Whenever terraform operation is run, terraform lock the statefile, so no other simultaneous operation can update statefile. and release the lock once operation is successful.
- during terraform plan/apply, the statefile is fteched to local from remote backend, modifies it if necessary during operation, upload it back to backend and the delete the file from local directory.

- If no backend is configured in terraform, terraform will use the default local backend, whih will store .tfstate file locally.
 
*Do its quiz again*
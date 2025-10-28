This page shall describe the steps needed to manipulate the go-dummy for test-cases and show-cases

# Preparation
In case you do not have a Go Development running, you need to install a minimum setup:
1. recommendation: Use VSCode as base
2. follow this instruction: https://learn.microsoft.com/en-us/azure/developer/go/configure-visual-studio-code

# Add a "fake" dependency
1. Create a test- or demo-branch acc. to the guidance in ../Tooling-Landscape/Dummy_Repositories/README.md
2. Select a dependency in https://pkg.go.dev/
3. Open the editor for the respective "*.go"-file in the branch
4. add the new dependency in the import section e.g. "rsc.io/quote"
5. save the file
6. Open the editor for the respective go.mod-file in the same folder than the "*.go"-file
7. add the new dependency in the first "require" section as direct dependency including the version you found in 2. e.g. rsc.io/quote v1.5.2
8. go back to the "*.go"-file, set a debug point and run the debugger => run and debug
9. (optional) the VSCode editor might already show "Problem" and indicate the line of the dependency with a yellow lightbulb => click on the bulb and perform "go get ..." => this might trigger a go to get the missing module
10. the debugger should indicate a "Build Error: ... missing go.sum entry for the newly introduced dependency => expected behaviour
11. open the terminal and browse to the Go-Dummy folder of the respective "*.go-" and go.mod-file
12. run the command "go mod tidy", that should trigger the download of the packages and update the go.sum-file, the download may take a while depending on the module as transitive dependencies will also be downloaded
13. re-do step 8. => the build should be successful - continue the run after the debug stop
14. commit your changes
15. push the changes to the repository
16. run a test with a SCA-tooling of your choice to check if the new dependency had to expected effect
17. document the testcase/democase in the respective doc/... branch including the expected result

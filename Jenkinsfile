//below libary name should match with jenkins Libary Name
@Library('jenkins-shared-library') _

def configMap = [

    project : "roboshop",
    componet: "catalogue"

]
//here it is refer main branch and it not allowed we have made all this in feature branch
echo "Going to execute Jenkins shared library"
// if branch is not equal to main, then run CI pipeline
if ( ! env.BRANCH_NAME.equalsIgnoreCase('main') ){
    nodeJSEKSPipeline(configMap)
}
else {
    echo "Please follow the CR process"
}
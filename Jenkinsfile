import jenkins.model.*

def GITURL = 'https://github.com/udaim2000/abap-rest-api.git'
def BRANCH = 'master'
def PIPELINE_GITURL = 'https://github.com/udaim2000/abap-ci-postman.git'
def PACKAGE = '''$REST_SIMPLE'''
def COVERAGE = 80
def VARIANT = "DEFAULT"

parallel (
    "EH7":{
        node {
        	def LABEL = "EH7"
        	def HOST = "eccides7.wdf.sap.com"
        	def CREDENTIAL = "EH7"
        	
        	git poll: true, branch: BRANCH, url: GITURL
        		
        	stage('[' + LABEL + '] Preparation') {
        		deleteDir()
        		dir('sap-pipeline') {
        			bat "git clone " + PIPELINE_GITURL + " ."
        		}
        	}
        	
        	def sap_pipeline = load "sap-pipeline/sap.groovy"
        	sap_pipeline.abap_unit(LABEL,HOST,CREDENTIAL,PACKAGE,COVERAGE)
        	sap_pipeline.abap_sci(LABEL,HOST,CREDENTIAL,PACKAGE,VARIANT)
        	sap_pipeline.sap_api_test(LABEL,HOST,CREDENTIAL)
        }
    }
    /* Add more system as needed...
	,"NPL":{
        node {
        	def LABEL = "NPL"
        	def HOST = "vhcalnplci.dummy.nodomain"
        	def CREDENTIAL = "NPL"
        	
        	git poll: true, branch: BRANCH, url: GITURL
        		
        	stage('[' + LABEL + '] Preparation') {
        		deleteDir()
        		dir('sap-pipeline') {
        			bat "git clone " + PIPELINE_GITURL + " ."
        		}
        	}
        	
        	def sap_pipeline = load "sap-pipeline/sap.groovy"
        	sap_pipeline.abap_unit(LABEL,HOST,CREDENTIAL,PACKAGE,COVERAGE)
        	sap_pipeline.abap_sci(LABEL,HOST,CREDENTIAL,PACKAGE,VARIANT)
        	sap_pipeline.sap_api_test(LABEL,HOST,CREDENTIAL)
        }
	} */
)
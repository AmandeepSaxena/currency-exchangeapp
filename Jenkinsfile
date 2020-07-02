pipeline{
	agent any
	stages{
		stage("Build"){
			steps{
				echo "Build"
			}
		}
		stage("Test"){
			steps{
				echo "Test"
			}
		}
		stage("Intergration Test"){
			steps{
				echo "Intergration Test"
			}
		}
	}
	post{
		always{
			echo "I am awesome, I always run"
		}
		success{
			echo "I run when you're successful"
		}
		failure{
			echo "I run when you fail"
		}
	}
}
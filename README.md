# Github workflows Android project

The Github actions have to be inside the `.github/workflows` folder, as it is in this repository.
For security reasons, the recommendations is about storing sensitive data like keystore, token etc. into Github actions secrets (./settings/secrets/actions). We don't keep them inside the project.

All the workflows target Java 17 because of Gradle 8.
The selected runner engine is Ubuntu, cheaper than macOS. 

## Pull requests
Default workflow triggered when you open a pull request.

The steps are :
- Checkout the project
- Setup the runner to Java 17 for Gradle
- Setup Gradle build tool
- Run tests on default flavour and Detekt for static analysis

## Firebase app distribution deployment
Deployment triggered by manual action or when a pull request has been mergd to the defined branch, here it's `main` branch.
We get the release note as input as specified on top.

The steps are :
- Checkout the project
- Setup the runner to Java 17 for Gradle
- Setup Gradle build tool
- Decode the keystore signing file
- Run tests on release flavour
- Assemble release
- Create a release note from the input
- Download the Firebase CLI
- Deploy the generated build into Firebase

## Google Play Store deployment
Deployment triggered by manual action.
We deploy the app as a draft to add a manual step at the end for deployment.

The steps are :
- Checkout the project
- Setup the runner to Java 17 for Gradle
- Setup Gradle build tool
- Decode the keystore signing file
- Run tests on release flavour
- Bundle release
- Create a release note from the input
- Deploy the bundle aab into Play Store as draft.


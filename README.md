RI-Challenge
===

# Prerequisites:

Make sure you have these installed and configured in your test machine:
1. Git
2. Docker
3. Kubectl
4. curl

# Installation:

- Clone git repository to the local machine:

    pwd
    git clone https://github.com/arathdeepak/RI-Challenge.git && cd RI-Challenge

- Edit below file and add any text to it.

    vi ./src/index.html

Add your text here:

    <body>
    <h2>Himalayan Affair</h2>

Or upload a new image and change here:

    <img src="himalayan.jpg"
    
Or add test anywhere you like.

- After finishing the edit, commit and push the code to git (Optional).

Follow the steps to push the code to git:

    git status
    git add .
    git commit -m "Commit message"
    git pull
    git remote -v
    git remote add origin git@github.com:arathdeepak/RI-Challenge.git
    git push -u origin master
    
- Do the following to build and push changes to Docker Hub with a VERSIONINFO:

        docker build --tag=arathdeepak/helloworld:VERSIONINFO .
        docker push arathdeepak/helloworld:VERSIONINFO

Then, Edit K8s file to add the new version number and other changes:

    vi ri-app-deploy.yaml 
    
New version here:
    
        spec:
      containers:
      - name: nxg
        image: arathdeepak/helloworld:VERSIONINFO

Make changes here if we need to scale the application:
    
    spec:
    replicas: Number-Of-Replicas
    selector:
    
Then:

    kubectl apply -f ri-app-deploy.yaml

Use below commnds to see the running status:

    kubectl get deploy
    kubectl get svc
    
### Test:

Open localhost in browser or do a curl for the output:

    curl http://localhost

## Recommendation for Production deployment:

1. Need to automate the build and deploy jobs via `Jenkins` and `Ansible` or via shell script.
2. We can pass version-info and replica details from jenkins as variables to the ansible job.
3. `CI/CD pipe line` and `test cases` can be executed from Jenkins.
4. `SonarCube` or similar tools can be used to analyze code quality from Jenkins.
5. Need to have an external IP and DNS to resolve the web application.
6. Geo location based `CDN` and an extra caching can be used for static contents.
7. Need to enable SSL for the domain.
8. An external reverse proxy can be used to improve security.
9. App scaling needs to be validated and auto-scaling can be implemented by setting thresholds.
10. Need to have monitoring mechanism to make sure uptime is 100%.


## Thanks for reading. The END!!


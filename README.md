# prod-cicd
robust CI/CD pipeline

### Step 1: Setup git repo
- Created git repository within github
- Clone your repo locally
	```shell
  ➜  prod-cicd git:(main) git clone https://github.com/mmontijo/prod-cicd.git
	```
- Add project files. I'll be using a snake game from this github repository: https://gist.github.com/ZiKT1229/5935a10ce818ea7b851ea85ecf55b4da
- Push local code to github
  ```bash
	➜  prod-cicd git:(main) git add .
	➜  prod-cicd git:(main) git commit -m "adding html snake to repo"
	➜  prod-cicd git:(main) git push
  ```
- Create a test branch
	```bash
	➜  prod-cicd git:(main) git branch test
	➜  prod-cicd git:(main) git checkout test
	```
- Make basic changes within test branch to check functionality.
	```html
  //////////////////////////////////////////////////////////////////////////////////////
  // CHANGE APPLE COLOR
  // draw applegit
  context.fillStyle = 'red';
  context.fillRect(apple.x, apple.y, grid-1, grid-1);
	```
- apply changes locally within the test branch
	```shell
	➜  prod-cicd git:(test) git add .        
	➜  prod-cicd git:(test) ✗ git commit -m "adding ////// to identify where to  change the color"
	➜  prod-cicd git:(test) git push
	```
- this gave me an error, mentioned error was fixed with:
	```shell
	➜  prod-cicd git:(test) git push --set-upstream origin test
	```
- push changes to main branch
	```shell
  ➜  prod-cicd git:(test) git checkout main
  ➜  prod-cicd git:(main) git merge test
  ➜  prod-cicd git:(main) git push
	```

---
### Step 2: Setup Jenkins (locally) COMPLETED

- install Java
	- I'm using pop-OS(Ubuntu distribution), java is already installed
- download the lts version of Jenkins
	```shell
  ➜  ~ sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
	https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
	```
- add the Jenkins repository to the local repository of Ubuntu
	```shell
  ➜  ~ echo "deb signed-by=/usr/share/keyrings/jenkins-keyring.asc" \
	https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
	/etc/apt/sources.list.d/jenkins.list > /dev/null
	```
- Update the apt package list
	```shell
	➜  ~ sudo apt-get update
	```
- install Jenkins and dependencies
	```shell
	➜  ~ sudo apt-get install jenkins
	```
- verify Jenkins version
	```shell
	➜  ~ jenkins --version
	```
- verify if Jenkins is running
	```shell
	➜  ~ sudo systemctl status jenkins
	```

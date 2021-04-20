## Project 4  
  
### Project Overview  
  
  Project 4 is a guide on how to set up a website and deploy it using Docker and AWS.

### Docker set up
  
  I installed Docker using the Desktop installer from the [Docker website](https://www.docker.com/products/docker-desktop).  I included the WSL2 dependencies because all of my interactions with Ubuntu would be through this.  
  In my project directory, I created a sub-directory called `html` where I placed the html files for my website.
  Next, I created a Dockerfile with the contents `FROM httpd:2.4 COPY ./html/ /usr/local/apache2/htdocs/`. This is is the file I used to build my container using the base Apache2 container and copy the contents of my `html` directory to the corect directory within the Apache container.  
  I used `docker build -t name:version .` to build my Docker container and give it a version number.  
  I used `docekr run -d -p 5000:80 name:version` to run my container.  This connected my local port 5000 to port 80 of the container.  
  To view the site running from the container, I just had to browse to `127.0.0.1:5000` in my browser of choice.  
    
### AWS CLI set up  
  
  Following [this guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html#cliv2-linux-install), I downloaded, unziped and installed the AWS Command Line Interface in WSL2.
  To configure AWS CLI, first I had to create the `.aws` directory and then create the `credentials` and `config` files in that directory.  
  In the `credentials` file, I entered the `aws_access_key_id` and the `aws_secret_access_key` provided by the AWS IAM service.  
  In the `config` file, I set `region=us-east-1` and `output=json` defaults.  
    
### ECR  
  
  `aws ecr create-repository --repository-name ceg3120/w013cfm --region us-east-1` is the command I used to create a repository.  
    
### GitHub Secrets  
  
  In the GitHub web interface, I accessed the Security --> Secrets section. There I created two repository secrets called `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` and entered the coresponding information into those secrets.

### GitHub Workflow  
  
  Using the sample Workflow provided, I changed the `AWS_REGION` to `us-east-1` and `ECR_REPOSITORY` to `ceg3120/w013cfm` as those were the region and name I had used when setting up my repository at an earlier stage. 
  I placed my new `docker-to-ecs.yml` Workflow into the `.github/workflows` directory within my project and pushed to GitHub, noting in the Actions tab has status updates for Workflow execustions.
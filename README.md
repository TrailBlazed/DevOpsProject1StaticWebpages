# DevOpsProject1StaticWebpages
## Steps :
### 1.Login from IAM
* Create **User** with S3FullAccess Policy.
* Download the Access Keys.

### Login with the User
* Create S3 bucket
* Go to **Permissions** -> Block public access (bucket settings) -> Edit ->Uncheck -> Block All Public Access
* Bucket policy ->Edit
<pre>
    {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<Bucket Name>/*"
        }
    ]
  }
  </pre>
  * Go to -> **Properties** -> Enable Static Website
  
  ### 2. Github Repo
  * Create a new Github Repo
  * Goto -> **Setting**
    * goto ->Secrets
    * New Repo Secrets -> AWS_Access_Key and AWS_Secret_Key(from the csv downloaded for the User)
  * Goto -> **Github Actions** -> New WorkFlow -> Create your own
    * RepoName/GitHub/workflow/main.yml 
    
    ```yml
    name: Static Website
    on:
        push:
    branches:
      - main
    jobs:
        staticwebsite_aws:
        runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v1

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
     aws-region
          aws-region: us-east-1

      - name: Deploy static site to S3 bucket
     Your bucker name
        run: aws s3 sync . s3://<BucketName> --delete
        
        
     ```
  
  
  

    

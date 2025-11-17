# CodePipeline Deployment Steps

## Prerequisites
1. GitHub repository: EvanLaksanaWP/cloudformation-cicd-mcr
2. CodeConnections connection already created
3. AWS CLI configured

## Step-by-Step Deployment

### 1. Deploy Dev Pipeline
```bash
aws cloudformation deploy \
  --template-file pipeline-dev.yaml \
  --stack-name web-pipeline-dev \
  --capabilities CAPABILITY_IAM
```

### 2. Deploy Prod Pipeline
```bash
aws cloudformation deploy \
  --template-file pipeline-prod.yaml \
  --stack-name web-pipeline-prod \
  --capabilities CAPABILITY_IAM
```

### 4. Trigger Deployments
- Push to `dev` branch → triggers dev pipeline → deploys to dev environment
- Push to `main` branch → triggers prod pipeline → deploys to prod environment

## Pipeline Flow
1. **Source**: GitHub webhook triggers on branch push
2. **Build**: CodeBuild uploads templates to S3 and deploys CloudFormation
3. **Deploy**: Infrastructure is created/updated with environment-specific naming

## Monitoring
- Check CodePipeline console for pipeline status
- Check CloudFormation console for stack deployment status
- Check outputs for ALB DNS names
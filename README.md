# Terraform Portfolio Project

A static portfolio website deployed on AWS using Terraform.

## What this project does

1. Takes a Next.js website and builds it into static HTML files
2. Uploads those files to AWS S3
3. Serves them globally through AWS CloudFront CDN

## How it works
Next.js app → npm run build → static HTML files
↓
AWS S3 (file storage)
↓
AWS CloudFront (global delivery)
↓
User sees the website

## Tech stack

- **Next.js** — React framework that builds the website into static files
- **AWS S3** — stores the static HTML, CSS and JS files
- **AWS CloudFront** — delivers files fast to users around the world
- **Terraform** — creates all AWS infrastructure automatically from code

## Project structure
terraform-portfolio-project/
├── nextjs-blog/          # Next.js website source code
│   ├── pages/            # website pages
│   ├── styles/           # CSS styles
│   └── out/              # built static files (not in git)
└── terraform-nextjs/     # infrastructure as code
├── backend.tf        # where Terraform stores its state
├── main.tf           # AWS resources to create
└── outputs.tf        # prints URLs after deployment

## How to deploy

### Requirements
- AWS CLI configured
- Terraform installed
- Node.js and npm installed

### Steps

**1. Build the website**
```bash
cd nextjs-blog
npm run build
```

**2. Deploy AWS infrastructure**
```bash
cd terraform-nextjs
terraform init
terraform apply
```

**3. Upload website files to S3**
```bash
aws s3 sync ../nextjs-blog/out s3://YOUR-BUCKET-NAME
```

**4. Open the website**

After `terraform apply` you will see:
cloudfront_url = "xxxxx.cloudfront.net"

Open that URL in your browser.

## How to destroy

To delete all AWS resources and stop paying:
```bash
terraform destroy
```

## Key concepts learned

- **Infrastructure as Code** — describe infrastructure in files instead of clicking in AWS console
- **Static Site Generation** — build HTML files once, serve them fast without a server
- **CDN** — serve files from servers close to the user for faster loading
- **S3 backend** — Terraform saves its state remotely so it remembers what it created
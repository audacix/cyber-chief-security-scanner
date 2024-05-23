# Cyber Chief API Security, Web App Security & CSPM Security Tool
by [Audacix](https://www.audacix.com/)


## Overview
This task allows you to run Cyber Chief Scans in your own GitHub Pipeline jobs.

There are 3 scan types to choose from:

- Web App Scan - Web app related scans
- Bolt API Scan - API endpoints related scans
- Raider CSPM - Cloud services related scans


## Prerequisites 
- you need to have a [Cyber Chief account](https://secure.cyberchief.ai/account/login/?next=/) before getting started.



## Getting started

### Note:
- GitHub Actions [pricing minutes](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions) apply 

### Notable Fields
- `target_url (required)` is the Automated Test URL in Cyber Chief
- `api_token (required)` is the API Token in Cyber Chief
- `fail_high (default: false)` and `fail_high_medium (default: false)` 
    - if set to `true`, the job:
        - waits for Cyber Chief scans to finish
        - fails the pipeline if vulnerabilities are found
        - show vulnerability details
    -  **If you're low on minutes, we suggest setting these to `false`**

### Running Web app scans
- `scope (default: reconnaissance, case-sensitive)`
    - choose either `reconnaissance`, `attack` or `infiltration`

```
steps:
  - name: Cyber Chief Security Scanner
    uses: audacix/cyber-chief-security-scanner@<version>      
    with:
      scan_type: "web"
      target_url: ""
      api_token: ""
      scope: ""
      fail_high:
      fail_high_medium:
```

### Running API scans
- `api_name (required, case-sensitive)`
    - The `API Name` set in Cyber Chief Bolt workspace admin

```
steps:
  - name: Cyber Chief Security Scanner
    uses: audacix/cyber-chief-security-scanner@<version> 
    with:
      scan_type: "api"
      target_url: ""
      api_token: ""
      api_name: ""
      fail_high:
      fail_high_medium:
```

### Running Raider scans
- `raider_name (required, case-sensitive)`
    - The `Raider Name` set in Cyber Chief Raider Workspace Admin
- `raider_type (required, case-sensitive)`
    - The Selected `Raider Cloud` in Cyber Chief Raider Workspace Admin
- `regions (required, case-sensitive)`
    - Input regions you want the Raider Scan to run
    - Regions for AWS Raider Type `(can have multiple inputs)`:
        ```
        us-east-1
        us-east-2
        us-west-1
        us-west-2
        af-south-1
        ap-east-1
        ap-southeast-1
        ap-southeast-2
        ap-southeast-3
        ap-south-1
        ap-northeast-1
        ap-northeast-2
        ap-northeast-3
        ca-central-1
        eu-central-1
        eu-central-2
        eu-west-1
        eu-west-2
        eu-west-3
        eu-south-1
        eu-south-2
        eu-north-1
        me-south-1
        me-central-1
        sa-east-1
        ```
    - Sample input:
        ```
        regions: "us-east-1, us-east-2, us-west-1, us-west-2"
        ```
    - Regions for Azure Raider Type `(only single input)`:
        ```
        AzureCloud
        AzureChinaCloud
        AzureUSGovernment
        AzureGermanCloud
        ```
    - Sample input:
        ```
        regions: "AzureCloud"
        ```
- `services (only applicable for raider_type = aws, case-sensitive)`
    - Note: Frameworks will be empty once you select anything in services
    - input services you want to scan
        ```
        accessanalyzer
        account
        acm
        apigateway
        apigatewayv2
        appstream
        autoscaling
        awslambda
        backup
        cloudformation
        cloudfront
        cloudtrail
        cloudwatch
        codeartifact
        codebuild
        config
        directoryservice
        drs
        dynamodb
        ec2
        ecr
        ecs
        efs
        eks
        elb
        elbv2
        emr
        fms
        glacier
        glue
        guardduty
        iam
        inspector2
        kms
        macie
        networkfirewall
        opensearch
        organizations
        rds
        redshift
        resourceexplorer2
        route53
        s3
        sagemaker
        secretsmanager
        securityhub
        shield
        sns
        sqs
        ssm
        ssmincidents
        Trustedadvisor
        vpc
        workspaces
        ```
    - Sample input:
        ```
        frameworks: "ecs, ec2, sqs"
        ```
- `frameworks (only applicable for raider_type = aws, case-sensitive)`
    - Note: Services will be empty once you select anything in frameworks
    - input frameworks you want to scan
        ```
        aws_audit_manager_control_tower_guardrails_aws
        aws_foundational_security_best_practices_aws
        aws_well_architected_framework_reliability_pillar_aws
        aws_well_architected_framework_security_pillar_aws
        cisa_aws
        cis_1.4_aws
        cis_1.5_aws
        cis_2.0_aws
        ens_rd2022_aws
        fedramp_low_revision_4_aws
        fedramp_moderate_revision_4_aws
        ffiec_aws
        gdpr_aws
        gxp_eu_annex_11_aws
        gxp_21_cfr_part_11_aws
        hipaa_aws
        iso27001_2013_aws
        mitre_attack_aws
        nist_800_53_revision_4_aws
        nist_800_53_revision_5_aws
        nist_800_171_revision_2_aws
        nist_csf_1.1_aws
        pci_3.2.1_aws
        rbi_cyber_security_framework_aws
        soc2_aws
        ```

    - Sample input:
        ```
        frameworks: "cisa_aws, gdpr_aws, ffiec_aws"
        ```

```
steps:
  - name: Cyber Chief Security Scanner
    uses: audacix/cyber-chief-security-scanner@<version> 
      scan_type: "raider"
      target_url: ""
      api_token: ""
      raider_name: ""
      scan_name: ""
      regions: ""
      services: ""
      frameworks: ""
      fail_high:
      fail_high_medium:
```

## Support
For support issues, please contact support@audacix.com.

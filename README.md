# AWS Setup

This is a collection of cloudformation templates, scripts and guides to prime
personal AWS accounts.

A lot of this guide will focus on general best-practise and what you can get
for free or is within the free-tier of AWS.

## Get out of the Root account!

Setup some methods to give yourself less elevated permissions.
Root access is cool and all but shouldn't be something you use all the
time or even have access keys for.

Before you leave it setup the following:

IAM
 - Root MFA!
 - Ensure there is no root credentials made

Billing page
 - Security questions, go for randomized answers
 - IAM access to billing

Finally, randomize the password and reset the password every time you go into
the root account. Cannot leak the root password if you lose it every time.

Now to access your account without root access you have a few choices of what to use:

 - IAM Users: simple, cli credentials are easy but long lived
     * Attach a policy of what you need
     * *Setup MFA!*
 - IAM Users + Assume roles:
     * Attached only allows `sts:AssumeRole` into defined roles for different
         permission levels (Developer, Admin, Billing, etc.)
     * Setup MFA!
 - SAML/OpenID identity provider
     * Single login
     * Uses federated roles
     * CLI credentials need external tooling
     * Remember to force Identity provider to have MFA
 - AWS SSO: First party approach
    * temporary CLI credentials are given on login
    * permission sets are cool
    * Needs to have Organisations enabled & AD server (not free tier friendly)

You can setup SAML/OpenID with Okta's free tier or if you have Google Apps.

## Cloudformation Templates

 * `sumologic-sns.yml` - Sets up integration to ingest Cloudtrail into Sumologic
     via SNS topic
 * `sumologic.yml` - Sets up integration to add a Cloudtrail source into
     SumoLogic

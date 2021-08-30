# [Bug Fix]Support for password authentication was removed on August 13, 2021

## Problem Description

When I tried to push my local repository to Github, I received the following error:

```shell
fatal: Could not read from remote repository. Please make sure you have the correct access rights and the repository exists.

remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.

remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.

fatal: unable to access 'https://github.com/niladmiran/niladmiran.github.io/': The requested URL returned error: 403
```

## Solution

1. Generate the token on Github, see [Generate personal Token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)
2. run the following command on command line:

```shell
git remote set-url origin https://<your_token>@github.com/<USERNAME>/<REPO>.git
```

where 

- `<your_token>` is the token you generated on Github
- `<USERNAME>` is the username of your Github
- `<REPO> ` is the username of your repository

 Actually, the url is simply obtained by inserting your token into the address of your repository, for example, my repository is :

`https://github.com/niladmiran/niladmiran.github.io.git`

my token is

`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n`

then the remote url is:

`https://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n@github.com/niladmiran/niladmiran.github.io.git`


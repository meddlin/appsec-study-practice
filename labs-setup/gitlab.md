# GitLab - Lab Setup

Here are a few resources I found useful while setting up my GitLab server. I won't say these are 
"best practices", but they are practices that worked for me. **Remember**, this a server for a 
lab setting. It *is not* publicly accessible, and is *not* serving a team for production-ready 
operations. 

Configure accordingly.

## Docker installation

[https://docs.gitlab.com/ee/install/docker.html](https://docs.gitlab.com/ee/install/docker.html)

### Vi Editor Tips

Most docker containers don't have text-based editors available other than vi. So, having a list of 
commands will be handy when/if making config changes inside of them is needed.

[https://www.redhat.com/sysadmin/introduction-vi-editor](https://www.redhat.com/sysadmin/introduction-vi-editor)

## Steps after installing GitLab

[https://docs.gitlab.com/ee/install/next_steps.html](https://docs.gitlab.com/ee/install/next_steps.html)

## Resetting Admin password

Reset GitLab CE administrator password via Ruby console

"exec" into container

```bash
sudo docker exec -it <container-id> sh
```

- `docker exec` examples: [https://docs.docker.com/engine/reference/commandline/exec/#examples](https://docs.docker.com/engine/reference/commandline/exec/#examples)


Once we have a shell in the container, start Rails console. 

```bash
sudo gitlab-rails console -e production
```

And reset the password...

```bash
## ...wait for console to start

# Find the root user
user = User.find_by_username 'root'

# Set a new password
new_password = 'securepassword' 
# You can get a random password with new_password = ::User.random_password
user.password = new_password
user.password_confirmation = new_password

# Save it
user.save!

# finally...
exit
```

From bitnami

- [https://docs.bitnami.com/aws/apps/gitlab/administration/reset-gitlab-admin-password/](https://docs.bitnami.com/aws/apps/gitlab/administration/reset-gitlab-admin-password/)

GitLab Docs

- [https://docs.gitlab.com/ee/security/reset_user_password.html#reset-your-root-password](https://docs.gitlab.com/ee/security/reset_user_password.html#reset-your-root-password)


## Configure Email

> NOTE: I don't have this working yet. This is just a collection of resources I've found useful so far.

GitLab docs, SMTP settings

- [https://docs.gitlab.com/omnibus/settings/smtp.html](https://docs.gitlab.com/omnibus/settings/smtp.html)

GitLab Docs, SMTP configuration examples: [https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/smtp.md#example-configuration](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/smtp.md#example-configuration)
- Specifically, this one example for Gmail: [https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/smtp.md#gmail](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/smtp.md#gmail)

This person had some challenges configuring GitLab to send email via Gmail SMTP, and there are some good tips in here: [https://forum.gitlab.com/t/using-gmail-to-send-email/710](https://forum.gitlab.com/t/using-gmail-to-send-email/710)
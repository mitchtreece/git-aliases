# Multiple git accounts

#### Step 1: Delete old ssh keys + generate new keys per account
ssh-keygen -t rsa -C "account1@email.com"
ssh-keygen -t rsa -C "account2@email.com"

#### Step 2: Copy keys, and add to git host
pbcopy < ~/.ssh/id_rsa_account1.pub
pbcopy < ~/.ssh/id_rsa_account2.pub

#### Step 3: Configure ssh hosts
cd ~/.ssh && touch config

Host account1
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_account1

Host account2
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_account2

#### Step 4: Update local identities, and check they were successfully stored
ssh-add -D
ssh-add id_rsa_account1
ssh-add id_rsa_account2
ssh-add -l

#### Step 5: Activate the keys with git host
ssh -T account1
ssh -T account2

#### Step 6: Add remote to repo
git remote add origin git@account1:gitusername/repo.git
git remote add origin git@account2:gitusername/repo.git

#### Note:
Make sure you're signing your commits with the proper user, the following git aliases help with this:

whoami = config user.email
account1 = config user.email \"account1@email.com\"
account2 = config user.email \"account2@email.com\"

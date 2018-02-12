# steemit-python Quickstart

This repo provides files and isntructions necessary to get the steemit-python library installed on a Codenvy debian workspace. It includes the Miniconda install script, to provide an up to date Python environment, and a patched version of steemit-python's METADATA file, to fix a dependency versioning issue.

## Install Miniconda

```
cd /projects/steem-python-setup
chmod u+x Miniconda3-latest-Linux-x86_64.sh

## Install Dependencies

```
sudo apt-get install build-essential libssl-dev
```

## Install steem-python

```
pip install steem
```

## Patch METADATA

steem-python wants toml 0.9.3.1, but pip installs 0.9.3. This will cause an error with the steempy command line tool when it does a dependency check, but it doesn't seem to cause any problems in practice. Simply modifying steem-python's version requirement to match the isntalled version fixes this for now. There's a patched version of the METADATA file in the repo that can be copied over the old one.

```
mv /home/user/miniconda3/lib/python3.6/site-packages/steem-0.18.103.dist-info/METADATA /home/user/miniconda3/lib/python3.6/site-packages/steem-0.18.103.dist-info/METADATA.bak
cp /projects/steem-python-setup/METADATA /home/user/miniconda3/lib/python3.6/site-packages/steem-0.18.103.dist-info/METADATA
```

## Set Node

The default nodes inlcuded with steem-python are no longer active. You can find the closest public nodes using [geo.steem.pl/](http://geo.steem.pl/). Then use steempy to set the node of your choice. For example, the Steemit API node over https:

```
steempy set node https://api.steemit.com:443
```

## Have some fun

Now we can launch python and play with the library a bit.

```
python
>>> from steem import Steem
>>> s = Steem()
>>> s.get_account('ned')['sbd_balance']
```
# dev-tools
developer productivity tools and one-off scripts

### Git Hooks
The `git-hooks` directory contains custom scripts that can help improve/simplify your git workflow. Copy any of the hooks you'd like into the `$PROJECT/.git/hooks` directory of your project and they will automatically fire at the correct git action. Make sure the file is executable so git can run it:
```
cd $PROJECT
chmod u+x .git/hooks/pre-commit
```
- **pre-commit**: Runs after you try to commit but before editing the commit message. Automatically lints all PHP files that have changed and adds them to the commit.

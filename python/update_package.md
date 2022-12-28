# How to update a new version of a package to GitHub and PyPI

Imagine there are two branches: building and master. In `main` branches only final, uploaded versions are commited, while `building` is used to build the new versions.

## Requirements

- GitHub user and repo
- `black`: code formatting
- `twine`: uploading to PyPI
- `setup.py` for the package with at least the basic information.
- PyPI user

## Steps

1. Being in `building` branch: Check that everything works in the new version.
2. Format the code by using `black`:
  ```bash
  black .
  ```
3. Modify the `setup.py` by changing the `version` number and the download link (keeping the chosen format for Git tags).
4. Commit the `setup.py` changes.
5. Change branch to `main` and merge from `building`:
  ```bash
  git checkout master
  git merge building
  ```
6. Create new tag for version `x.y.z` and upload it to GitHub:
  ```bash
  git tag x.y.z
  git push --tag
  ```
7. Go to repo homepage in [Github](https://github.com). Create a new release from the last tag (the one uploaded in the last step) and call it `x.y.z` (it has to have the same name that the tag).
8. Go back to `terminal`.
9. Create new version distribution:
  ```bash
  python setup.py sdist
  ```
10. Upload new version to pypi.org:
  ```bash
  twine upload dist/*
  ``` 
11. Go back to `building` branch and merge from `main`. Nothing should be merged:
  ```bash
  git checkout building
  git merge master
  ```
  

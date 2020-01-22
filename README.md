# Howie's Notes Source Code

## Init

1. `git clone -b source --recursive git@github.com:howiezhao/howiezhao.github.io.git`
2. `cd howiezhao.github.io`
3. `npm install`

Then you can build and run:

1. `hexo g`
2. `hexo s`

## Push

If the submodule is modified, push the submodule **first**:

1. `cd themes/hexo-theme-next`
2. `git add .`
3. `git commit -m "modify submodule"`
4. `git push`

Then push this repository:

1. `cd ../..`
2. `git add .`
3. `git commit -m "update the repository"`
4. `git push`

## Pull

1. `git pull`
2. `git submodule update --remote`

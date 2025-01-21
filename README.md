# 

Use conan recipes from git repos.

Put the below in `source()` and run `conan source .` 

You can place the gitrecipes.py in some local directory 
` wget -O scripts/gitrecipes.py https://raw.githubusercontent.com/kolbbond/conan-git-recipes/refs/heads/master/gitrecipes.py `
You can download within conanfile.py and import with 

```
        # download helper file dynamically  
        download(  
            conanfile=self,  
            url="https://raw.githubusercontent.com/kolbbond/conan-git-recipes/refs/heads/master/gitrecipes.py",  
            filename=".recipes/gitrecipes.py",  
        )  
        # dynamically load  
        # from importlib.machinery import SourceFileLoader  
        pkg = SourceFileLoader("gitrecipes", ".recipes/gitrecipes.py").load_module()  
```

Then to call and checkout recipes "corrade" and "magnum"  
`checkout()` adds a new local remote "conan_example" to conan (check with `conan list`)

``` 
        # setup repo and recipe directory (source), target directory, and remote name
        gr = pkg.GitRecipes(  
            cf=self,  
            url="https://github.com/kolbbond/conan-center-index.git",  
            source="recipes",  
            target=".recipes",  
            remotename="conan_example"
        )  
        gr.add_checkout("corrade")  
        gr.add_checkout("magnum")  

        gr.checkout()  
```


# 

Use conan recipes from git repos.

Put the below in `source()`

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

Then to call 

``` 
        # setup repo and recipe directory (source) and target directory
        gr = pkg.GitRecipes(  
            cf=self,  
            url="https://github.com/kolbbond/conan-center-index.git",  
            source="recipes",  
            target=".recipes",  
        )  
        gr.add_checkout("corrade")  
        gr.add_checkout("magnum")  
        gr.checkout()  
```

# SCSS/CSS Style Guide

##Twitter Bootstrap
The current version of bootstrap is 3.1.1.  To view the documentation,
go to http://getboostrap.com.  If the current version on
getbootstrap.com is greater than 3.1.1, you can 
download the documentation from here:
https://github.com/twbs/bootstrap/tree/v3.1.1 and run it locally. When
you receive a PSD/comp from creative, check the bootstrap documentation
to see if any components already exist in bootstrap before creating your
own.  Most of the time you should be able to use one of the existing
components and override any specific 
styling in the PSD.  Also, check the existing *.scss files, more than
likely the CSS for your module already exists in the project.  


##frontend_engine
The frontend_engine repo contains the common scss files for all
projects.  

During development, this project can be cloned to your local environment
and then symlink-ed in the stylesheets directory (make sure you pull
latest).  If you clone the project as a
sibling to the project, the symlink should be created in a linked_lib
directory in your project:

```
ln -s ../frontend_engine
```

The engine contains a bootstrap directory.  The only file that is
modified from the original bootstrap source is the _variables.scss.
This file has been updated with the Payoff 
default SASS variables and should not be modified.  If you need to
override the default SASS variables for a project, create a
_variables.scss in your project and @import it 
instead of the @import "frontend_engine/bootstrap/variables"; in the
bootstrap.scss file in your project.  Also, if you need to update the
styles in the _bootstrap_overrides.scss 
file without affecting the default styles, create a copy of the file in
your project and include it instead of the one in the engine.

Any changes made to the files in the frontend_engine will be reflected
in all projects.  So, make sure you need it in all projects and if you
make a change, be sure to regress your 
changes in all of the projects.  If you have specific styles for your
project, they should be in the root of the stylesheets directory.  


##File Naming
Root scss files that will be compiled into css files should be named
filename.css.css.  If the file is a partial and only gets included with
an @import, prefix the name with an 
underscore and do not add the ".css" to the file name: _my_partial.scss  


##Nesting and line breaks
Nest your CSS/SCSS rules under the parent class for the controller/page,
module:

good:

```
.page {
  .module {
    border: 1px solid #000;

    .title {
      font-weight: bold;
    }
  }
}
```

bad:

```
.page .module {
  border: 1px solid #000;
}

.page .module .title {
  font-weight: bold;
} 
```

Place the properties for your selectors before any descendant nested
selectors:

good:

```
.page {
  .module {
    border: 1px solid #000;

    .title {
      font-weight: bold;
    }
  }
}
```

bad:

```
.page {
  .module {
    .title {
      font-weight: bold;
    }
    
    border: 1px solid #000;
  }
}
```

Insert a line break between properties and nested selectors:

good:

```
.page {
  .module {
    border: 1px solid #000;

    .title {
      font-weight: bold;
    }
  }
}
```

bad:

```
.page {
  .module {
    .title {
      font-weight: bold;
    }    
    border: 1px solid #000;
  }
}
```  


##Selector Specificity 
* Avoid qualifying your selectors with too many classes/elements.  When
  possible, try to only go 3 deep.  This means that when you nest your
css classes, avoid nesting more than 3 deep as well.
* Avoid using id (#) selectors. ID selectors cause the selectors to have
  a higher specificity and make it harder to override the selector if
necessary.
* `!important` should be avoided whenever possible as it also causes a
  higher specificity, even higher than a `style` attribute.   


##Property Order
CSS/SCSS properties should be placed in alphabetical order for
consistency (better for gzip compression) and to make it easier to find
properties that are assigned:

good:

```
.module {
  background: #000;
  color: #fff;
  @import size(10px, 20px);
  text-transform: uppercase;  
} 
```

bad:

```
.module {
  text-transform: uppercase;
  @import size(10px, 20px);
  color: #fff; background: #000;
  background: #000;
}
```  


##Vendor Specific Properties
Use mixins for vendor specific properties:

good:

```
.paycon-refresh {
  @include animation(rotation 2s infinite linear);
}
```

bad:

```
.paycon-refresh {
  -webkit-animation: rotation 2s infinite linear;
  animation: rotation 2s infinite linear;
}
```  


##Class Naming
When naming CSS classes, use hyphens to separate class names.  Do not
use titlecase, camel case or underscores:

good:

```
.account-table {}
```

bad:

```
.account_table {}
.accountTable {}
.AccountTable {} 
```

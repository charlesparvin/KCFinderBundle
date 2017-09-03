KCFinderBundle for Symfony2 - Based on [KCFinder 3.1.2](http://kcfinder.sunhater.com)

Fork based on [Charles's modifications](https://github.com/charlesparvin/KCFinderBundle) to [OwenRay's modifications](https://github.com/OwenRay/KCFinderBundle) to [jocelynkerbourch's original bundle]( https://github.com/jocelynkerbourch/KCFinderBundle)

###Installation
Add to `composer.json`
```
"require": {
    "cautbur/kc-finder-bundle": "dev-master"
},
"repositories": [
    {
        "url": "https://github.com/cautbur/KCFinderBundle.git",
        "type": "git"
    }
]
```

Run `composer update`

Add to `app/AppKernel.php`
```
    new cautbur\KCFinderBundle\KCFinderBundle(),
```

###Configuration
Add to `app/config/routing.yml`:
```
kc_finder: 
    resource: "@KCFinderBundle/Resources/config/routing.yml" 
    prefix: /admin
```

Add to `app/config/config.yml` (configure upload directory as needed and don't forget to make it writable)
```
kc_finder:
    upload_url: "/uploads/images_articles"
    upload_dir: "%kernel.root_dir%/../web/uploads/images_articles"
```

Add to `app/config/security.yml` (or whatever permissions are required for your app)
```
security:
    access_control:
        - { path: ^/admin/kcfinder*, role: ADMIN }
```

###Integrating KCFinder with editors

Check [the official KCFinder documentation](http://kcfinder.sunhater.com/integrate)

####Example Integration with TinyMCE 4

Add this to your `tinymce.init` call :
```
tinymce.init({
    // ...
    file_browser_callback: function(field, url, type, win) {
        tinyMCE.activeEditor.windowManager.open({
            file: '/admin/kcfinder/browse.php?opener=tinymce4&field=' + field + '&type=' + type,
            title: 'KCFinder',
            width: 700,
            height: 500,
            inline: true,
            close_previous: false
        }, {
            window: win,
            input: field
        });
        return false;
    }
});
```

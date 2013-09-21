On the homepage, AdaptCMS will get the newest articles. You can loop through articles like so:

    <?php if (!empty($articles)): ?>
        <?php foreach($articles as $item): ?>
            <?php echo $item['Article']['title'] ?>
        <?php endforeach ?>
    <?php endif ?>

To display a no items found message, simply do this

    <?php if (empty($articles)): ?>
        No Articles found
    <?php else: ?>
        <?php foreach($articles as $item): ?>
            <?php echo $item['Article']['title'] ?>
        <?php endforeach ?>
    <?php endif ?>

For a full list of article tags you may use, see below.

* Article Name `<?php echo $articles['Article']['title'] ?>`
* Article Slug `<?php echo $articles['Article']['slug'] ?>`
* Article Created Datetime `<?php echo $articles['Article']['created'] ?>`
* Article Published Datetime `<?php echo $articles['Article']['publish_time'] ?>`
* Category Name `<?php echo $articles['Category']['title'] ?>`
* Category Slug `<?php echo $articles['Category']['slug'] ?>`
* Article Author Username `<?php echo $articles['User']['username'] ?>`
* Article Author Email `<?php echo $articles['User']['email'] ?>`
* Article Comment Count `<?php echo $articles['Comments'] ?>`

Custom Fields
-------------

For reference, check the custom fields section in the admin panel to find the specific list of fields for this category. The below examples are used in conjuction with a foreach above.
To use a custom field, simply do this:

`<?php echo $item['Data']['field-slug'] ?>`

Replace 'field-slug' with the slug of the field. (so System becomes system and Test This becomes test-this) To return the contents of a custom field if it is not a required field, do this:

<?php if (!empty($item['Data']['field-slug'])): ?>
    <?php echo $item['Data']['field-slug'] ?>
<?php endif ?>

This will render the custom field data if it is not empty. If you have a multi-option custom field, then the data will be in an array format. To loop through you can do this:

    <?php if (!empty($item['Data']['field-slug'])): ?>
        <?php foreach($item['Data']['field-slug'] as $field): ?>
            <?php echo $field ?>
        <?php endforeach ?>
    <?php endif ?>

This will check to see if the data is not empty and if so, loop through it. If you are not familiar with the foreach loop, you may want to read up on it at [php.net](http://www.php.net/manual/en/control-structures.foreach.php).

Tags
----

Similar to the above code block, you can easily go through article tags like so:

    <?php if (!empty($item['Article']['tags'])): ?>
        <?php foreach($item['Article']['tags'] as $tag): ?>
            <?php echo $tag ?>
        <?php endforeach ?>
    <?php endif ?>

To build a list that links to these tags (which is a category list type view, all articles showing with the specified tag), you can use this:

    <?php if (!empty($item['Article']['tags'])): ?>
        <?php foreach($item['Article']['tags'] as $tag): ?>
            <?= $this->Html->link('<span class="btn btn-success">' . $tag . '</span>', array(
                'controller' => 'articles',
                'action' => 'tag',
                $tag
            ), array('class' => 'tags', 'escape' => false)) ?>
        <?php endforeach ?>
    <?php endif ?>

Related Articles
----------------

Lastly, there are scenarios where you want to show related article data. For example, when viewing a game page you would want to show the system name for example.
If you have the two linked together, you can try showing the name like so if you expect only one item linked to it:

    <?php if (!empty($item['RelatedArticles']['category']['platforms'][0])): ?>
        <?php echo ($item['RelatedArticles']['category']['platforms'][0]['Article']['title'] ?>
    <?php endif ?>

You can see where the syntax follows the above with the `['Article']['title']` bit. The same you see above is accessible from a related article. If you believe there are multiple
relationships, you can list them out:

    <?php if (!empty($item['RelatedArticles']['category']['platforms'])): ?>
        <?php foreach($item['RelatedArticles']['category']['platforms'] as $item): ?>
            <?php echo $item['Article']['title'] ?>
        <?php endforeach ?>
    <?php endif ?>

For the above two examples, the platforms is the slug of the category, replace that with whatever category of related items you wish to show or if you want to list all related items -
replace `['category']['platforms']` with `['all']`.
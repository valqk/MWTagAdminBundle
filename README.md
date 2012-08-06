The goal of this bundle is to make it easy to use the FPNTagBundle together with the SonataAdminBundle.

In your entities:

``` php
class ...
{
    use \MW\Bundle\TagAdminBundle\Entity\Traits\Tagging;
    ...
}
```

In your admin classes:

``` php
class ...Admin extends Admin
{
    use \MW\Bundle\TagAdminBundle\Admin\Traits\TagHandler;

    ...

    protected function configureFormFields(FormMapper $formMapper)
    {
        $formMapper
            ...
            ->add('tags_plain', 'textarea')
            ->end()
            ;
        }
    }
    ...
}
```

In your service definitions:

``` xml
<service id="..." class="...">
    <tag name="sonata.admin" manager_type="..." group="..." label="..."/>
    <argument />
    <argument>...</argument>
    <argument>...</argument>
    <call method="setTagTransformer">
        <argument type="service" id="mw.text_to_tag_transformer" />
    </call>
</service>
```
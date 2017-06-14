.. _adding_localiz:

Adding Localizations (i18n)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Digital Rebar uses the Rails I18N library.  Please refer to the
documentation `guides <http://guides.rubyonrails.org/i18n.html>`_ for usage hints
that can help reduce coding, and to add features such as
Interpolation.

Each barclamp is expected to add its own localization (i18n) file.

\ **Note**: Please do *not* add localizations into another
barclamp's i18n file.  Also, take care to not create duplicate
entries; doing so can confuse Digital Rebar.

1. Add the localization file (``en.yml`` is the default) into the
   ``rebar_framework/config/locales/[barclamp]`` directory. 
   
   \ **Note**: Replace [barclamp] with the name of the barclamp.

2. If supporting multiple languages, replace ``en`` with the
   target language code.  For example, use ``fr.yml`` for a French translation.  

3. Inside the i18n file, provide a simple YML hash for translations.  For
   example:

   .. raw:: html

      <pre>en:
        # Layout
        nav:
          nodes: Nodes
          nodes_description: Infrastructure Components</pre>

   \ **Note**: Encode the translations in quotes if
    comma ( : ) or tick ( \` ) characters are needed!

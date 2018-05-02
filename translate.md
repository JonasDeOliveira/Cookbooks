## Traduzindo arquivos JavaScript no Magento.

Neste tutorial mostrarei como aplicar os padrões de internacionalização do Magento em arquivos JavaScript.

Bom, primeiro configure o seu arquivo de tradução no **_config.xml_** que fica em:  
app/code/codepool/NameSpace/ModuleName/etc/config.xml

```
<?xml version="1.0"?>
<config>
    <modules>
        <NameSpace_ModuleName>
            <version>1.0.0.0</version>
        </NameSpace_ModuleName>
    </modules>
    <frontend>
        <translate>
            <modules>
                <NameSpace_ModuleName>
                    <files>
                        <default>NameSpace_ModuleName.csv</default>
                    </files>
                </NameSpace_ModuleName>
            </modules>
        </translate>
    </frontend>
</config>
```
Coloque o nome do seu arquivo de tradução dentro da tag **_<default>_**, colocando o Name Space e o nome do módulo como no exemplo acima.


Crie um arquivo chamado **_jstranslator.xml_** em:
app/code/codepool/NameSpace/ModuleName/etc/jstranslator.xml
```
<?xml version="1.0"?>
<jstranslator>

    <!-- jsfilename.js →

    <error_message translate="message" module="modulename">
        <message>Error reported</message>
    </error_message>

    <success_message translate="message" module="modulename">
        <message>Successfully registered</message>
    </success_message>

    <thank_message translate="message" module="modulename">
        <message>Thank you for registering</message>
    </thank_message>

    <!-- end jsfilename.js →

</jstranslator>
```
Repare que as tags **_<error_message>_**, **_<success_message>_** e **_<thank_message>_**, servem apenas para a sua organização ou seja, você determina os nomes de acordo com a sua organização, se você colocar **_<message_error>_** também irá funcionar.

Em **_translate="message"_** indica a tag que será traduzida, nesse caso <message>.

Em **_module="modulename"_** coloque o nome do seu módulo com todas as letras minúsculas.

Dentro da tag **_<message>_**, coloque a mensagem que irá ser traduzida em inglês.


Agora crie o arquivo csv que você configurou no **_config.xml_** e coloque as mensagens que você quer traduzir e a tradução separados por aspas duplas e vírgula, como no exmplo abaixo:

app/locale/pt_BR/NameSpace_ModuleName.csv
```
"Error reported","Erro relatado"
"Successfully registered","Registrado com sucesso"
"Thank you for registering","Obrigado por se registrar"
```

Por fim, em seu arquivo JS coloque a string que você deseja traduzir dentro de **_Translator.translate(‘ ’)_**, como no exmplo abaixo:

```
errorMessage: function() {
   return Translator.translate('Error reported');
},
successMessage: function() {
    return Translator.translate('Successfully registered');
},
thankMessage: function() {
    return Translator.translate('Thank you for registering');
}
```
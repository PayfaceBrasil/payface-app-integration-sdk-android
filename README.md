# Payface App SDK Android

Payface App SDK para Android fornece um SDK nativo para integração com o Payface App. Você pode usar o SDK para integrar o Payface nos seus aplicativos personalizados.

Para notas de lançamento, consulte [CHANGELOG.md](https://github.com/PayfaceBrasil/payface-app-integration-sdk-android/blob/master/CHANGELOG.md).

## Requisitos
**Versão**
minSdkVersion 21
targetSdkVersion 29

## Como Usar

Adicionar o AAR na pasta lib do projeto android:
*[PROJETO]/app/libs* 

No build.gradle do app no contexto android adicionar a seguinte configuração:

```
android {
    .
    .
    .
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}

```

Adicionar as seguintes dependencias:

```
dependencies {
    implementation files('libs/payface-app.aar')

    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    implementation 'com.google.android.material:material:1.2.0'
    implementation "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
    implementation 'androidx.legacy:legacy-support-v4:1.0.0'
    implementation 'androidx.navigation:navigation-fragment-ktx:2.3.0'
    implementation 'androidx.navigation:navigation-ui-ktx:2.3.0'

    def camerax_version = "1.0.0-beta07"
    // CameraX core library using camera2 implementation
    implementation "androidx.camera:camera-camera2:$camerax_version"
    // CameraX Lifecycle Library
    implementation "androidx.camera:camera-lifecycle:$camerax_version"
    // CameraX View class
    implementation "androidx.camera:camera-view:1.0.0-alpha14"
}
```

Compile o projeto para realizar a integração via código.

**Integração no código:**
```
    import br.com.payface.hybrid.HybridActivity
    .
    .
    .
    val hybridActivity =  Intent(this, HybridActivity::class.java)
    val partner = ""
    val cpf = ""
    val name = ""
    val cellphone = ""
    val button = "Voltar para aplicação"

    hybridActivity.putExtra("partner", partner)
    
    hybridActivity.putExtra("cpf", cpf)
    hybridActivity.putExtra("name", name)
    hybridActivity.putExtra("cellphone", cellphone)
    //Se não tiver a proxima linha, botão de voltar não aparecerá.
    hybridActivity.putExtra("button", button)

   startActivity(hybridActivity)
```

Observação
1. Para utilizar os pârametros do usuário, é necessário preencher pelo menos o CPF.

2. Caso o valor de **button** não seja configurado, o botão de voltar para a aplicação raiz não aparecerá. Para voltar será preciso utilizar o botão do android nativo.

## Serviços Suportados

Acesso ao app web Payface com utilização da câmera nativa Android.


## Relatar um Problema

Se você encontrar um problema com o Payface App SDK Android, pesquise as [issues existentes](https://github.com/PayfaceBrasil/payface-app-integration-sdk-android/issues)
e tente se certificar de que seu problema ainda não existe antes de [abrir uma nova issue](https://github.com/PayfaceBrasil/payface-app-integration-sdk-android/issues/new). É útil incluir a versão do SDK, ambiente e sistema operacional que você está usando. Inclua também um stack trace e os passos necessários para reproduzir o cenário.

## Licença

Consulte [LICENSE.md](https://github.com/PayfaceBrasil/payface-app-integration-sdk-android/blob/master/LICENSE.md) e [NOTICE.md](https://github.com/PayfaceBrasil/payface-app-integration-sdk-android/blob/master/NOTICE.md) para mais informações.

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

    implementation 'androidx.constraintlayout:constraintlayout:2.0.4'
    implementation 'com.google.android.material:material:1.2.0'
    implementation "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
    implementation 'androidx.legacy:legacy-support-v4:1.0.0'
    implementation 'androidx.navigation:navigation-fragment-ktx:2.3.2'
    implementation 'androidx.navigation:navigation-ui-ktx:2.3.2'

    def camerax_version = "1.0.0-rc01"
    // CameraX core library using camera2 implementation
    implementation "androidx.camera:camera-camera2:$camerax_version"
    // CameraX Lifecycle Library
    implementation "androidx.camera:camera-lifecycle:$camerax_version"
    // CameraX View class
    implementation "androidx.camera:camera-view:1.0.0-alpha20"
    
    //FaceDetector
    implementation 'com.google.android.gms:play-services-mlkit-face-detection:16.1.1'
}
```
No proguard-rules.pro adicionar a seguinte configuração 

```
-keep class br.com.payface.**  { *; }
-keep class androidx.fragment.app.**  { *; }
```

Compile o projeto para realizar a integração via código.

**Integração no código:**

**Por frame**

Nessa maneira você tera maior liberdade de adicionar customização em sua activity, por exemplo adicionar ToolBar, mudar cores de ToolBar e StatusBar.

No XML de sua activity colocar o container para aparecer o frame. A referencia para classe é **br.com.payface.hybrid.HybridFrameFragment**
```
 <androidx.fragment.app.FragmentContainerView
    android:id="@+id/hybrid_fragment_container"
    android:name="br.com.payface.hybrid.HybridFrameFragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
```

Enviar dados para o Frame através do Bundle

```
  val bundle = Bundle()
  bundle.putString("partner", "Nome do Partner")
  bundle.putSerializable("environment", HybridFrameFragment.Environment.PRODUCTION);
  bundle.putString("cpf", "numero cpf")
  bundle.putString("name", "Nome do usuário")
  bundle.putString("cellphone", "número do celular")

  val fm = this.supportFragmentManager
  val hybridFragment = fm.findFragmentById(R.id.hybrid_fragment_container)!!
  hybridFragment.arguments = bundle
```

Controle da webview através do back button nativo do android: 

```
override fun onBackPressed() {
   FragmentManager fm = this.getSupportFragmentManager();
   Fragment hybridFragment = fm.findFragmentById(R.id.hybrid_fragment_container);
   assert hybridFragment != null;

   if (!((HybridFrameFragment) hybridFragment).backNavigation())
      super.onBackPressed();
}
```

Observação
1. Para utilizar os pârametros do usuário, é necessário preencher pelo menos o CPF.

2. Para utilizar o ambiente sandbox basta passar como environment o valor HybridFrameFragment.Environment.SANDBOX no bundle. Para produção enviar o valor HybridFrameFragment.Environment.PRODUCTION.

## Serviços Suportados

Acesso ao app web Payface com utilização da câmera nativa Android.


## Relatar um Problema

Se você encontrar um problema com o Payface App SDK Android, pesquise as [issues existentes](https://github.com/PayfaceBrasil/payface-app-integration-sdk-android/issues)
e tente se certificar de que seu problema ainda não existe antes de [abrir uma nova issue](https://github.com/PayfaceBrasil/payface-app-integration-sdk-android/issues/new). É útil incluir a versão do SDK, ambiente e sistema operacional que você está usando. Inclua também um stack trace e os passos necessários para reproduzir o cenário.

## Licença

Consulte [LICENSE](https://github.com/PayfaceBrasil/payface-app-integration-sdk-android/blob/master/LICENSE) e [NOTICE](https://github.com/PayfaceBrasil/payface-app-integration-sdk-android/blob/master/NOTICE) para mais informações.

# TP3

## Exercice 1:

 ### Créez votre premier visuel d'interface graphique
 
 1. Où est décrite l'interface graphique ?
 
Il faut aller dans le dossier `res` et ouvrir un fichier XML

 2. Où est stocké le nom de votre application ? (Qui est affiché )

dans le fichier `activity_main.xml` 

        <?xml version="1.0" encoding="utf-8"?>  
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"  
      package="com.example.sudo">  
      
        <application  
      android:allowBackup="true"  
      android:icon="@mipmap/ic_launcher"  
      android:label="@string/app_name"  
      android:roundIcon="@mipmap/ic_launcher_round"  
      android:supportsRtl="true"  
      android:theme="@style/AppTheme">  
            <activity android:name=".MainActivity">  
                <intent-filter>  
                    <action android:name="android.intent.action.MAIN" />  
      
                    <category android:name="android.intent.category.LAUNCHER" />  
                </intent-filter>  
            </activity>  
        </application>  
      
    </manifest>

3. Modifiez le programme pour que le seul texte affiché soit "Un petit pas pour l'homme, un grand pas pour ma compréhension d'Android."

*rajouter image plus tard*

4. Complétez et modifiez l'interface graphique pour quelle ressemble à celle présentée en Illustration 1. Exemple de grandes étapes qui peuvent y mener (Illustration 2) :

*rajouter image plus tard*


### Ajouter des interactions

On va faire en sorte que le bouton change le texte du haut.

    package com.example.sudo;  
      
    import androidx.appcompat.app.AppCompatActivity;  
      
    import android.os.Bundle;  
    import android.view.View;  
    import android.widget.Button;  
    import android.widget.TextSwitcher;  
    import android.widget.TextView;  
      
    public class MainActivity extends AppCompatActivity {  
      
        Button changeTextButton;  
        TextView message;  
      
        @Override  
      protected void onCreate(Bundle savedInstanceState) {  
            super.onCreate(savedInstanceState);  
            setContentView(R.layout.activity_main);  
            message = (TextView)findViewById(R.id.text_V_h);  
            changeTextButton = (Button) findViewById(R.id.button_page_1);  
            changeTextButton.setOnClickListener(new View.OnClickListener(){  
            @Override  
      public void onClick(View v){  
                    message.setText("Bravo tu un sorcier Harry!");  
            }  
            });  
        }  
    }



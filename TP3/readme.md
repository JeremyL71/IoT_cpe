
# TP3

## Exercice 1:

 ### Créez votre premier visuel d'interface graphique
 
 1. Où est décrite l'interface graphique ?
 
Il faut aller dans le dossier `res` et ouvrir un fichier XML

 2. Où est stocké le nom de votre application ? (Qui est affiché )

dans le fichier `activity_main.xml` 
``` xml
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
```
3. Modifiez le programme pour que le seul texte affiché soit "Un petit pas pour l'homme, un grand pas pour ma compréhension d'Android."

*rajouter image plus tard*

4. Complétez et modifiez l'interface graphique pour quelle ressemble à celle présentée en Illustration 1. Exemple de grandes étapes qui peuvent y mener (Illustration 2) :

*rajouter image plus tard*


### Ajouter des interactions

On va faire en sorte que le bouton change le texte du haut.

``` java
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
```

## Exercice 2:
### Version simple (1 sonde)
Faites une application affichant les données lues sur les 3 axes de l'accéléromètre. Démarche possible :
- Réutilisez votre programme de l'exercice 1
- Implémentez l'interface SensorEventListener depuis l'activité ;
http://developer.android.com/reference/android/hardware/SensorEventListener.html
- Récupérez une référence vers le gestionnaire de services ;
Aide : (SensorManager)getSystemService(Context.SENSOR_SERVICE)
http://developer.android.com/reference/android/hardware/SensorManager.html
- Enregistrez l'activité en tant qu'écouteur pour le capteur voulus auprès du gestionnaire de service lors de la reprise et la dé-enregistrer à la mise en pause ;
Note : pensez à choisir une fréquence de rafraîchissement pas trop rapide.
Aides :
	- sm.registerListener(....) : Méthode d'enregistrement
	- sm.getDefaultSensor(Sensor.TYPE_ACCELEROMETER) : Choix d'un capteur
	- SensorManager.SENSOR_DELAY_UI : une fréquence de rafraichissement de l'interface graphique
- Faites en sorte que les valeurs reçues par onSensorChanged soient publiées sur l'interface graphique.

``` java
package fr.morandet.helloworld;

import androidx.appcompat.app.AppCompatActivity;

import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity implements SensorEventListener {

    Button changeTextButton;
    TextView textHint;

    SensorManager mSensorManager;
    Sensor mAccelerometer;
    TextView lblx;
    TextView lbly;
    TextView lblz;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        changeTextButton = (Button)findViewById(R.id.changeTextButton);
        changeTextButton.setOnClickListener(new View.OnClickListener(){
            @Override
            public void onClick(View v){
                textHint = (TextView)findViewById(R.id.textHint);
                textHint.setText("Alors ? C'est pas bô ça ? :D");
            }
        });

        mSensorManager = (SensorManager)getSystemService(SENSOR_SERVICE);
        mAccelerometer = mSensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);
        mSensorManager.registerListener(this, mAccelerometer, SensorManager.SENSOR_DELAY_NORMAL);
    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int accuracy) {}

    @Override
    public void onSensorChanged(SensorEvent event) {
        lblx = (TextView)findViewById(R.id.lblx);
        lbly = (TextView)findViewById(R.id.lbly);
        lblz = (TextView)findViewById(R.id.lblz);
        lblx.setText(String.valueOf(event.values[0]));
        lbly.setText(String.valueOf(event.values[1]));
        lblz.setText(String.valueOf(event.values[2]));
    }
}
```
``` xml
<?xml version="1.0" encoding="utf-8"?>  
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"  
  xmlns:app="http://schemas.android.com/apk/res-auto"  
  xmlns:tools="http://schemas.android.com/tools"  
  android:layout_width="match_parent"  
  android:layout_height="match_parent"  
  tools:context=".MainActivity">  
  
 <LinearLayout  
  android:layout_width="0dp"  
  android:layout_height="wrap_content"  
  android:orientation="horizontal"  
  app:layout_constraintBottom_toBottomOf="parent"  
  app:layout_constraintEnd_toEndOf="parent"  
  app:layout_constraintStart_toStartOf="parent"  
  app:layout_constraintTop_toTopOf="parent">  
  
 <TextView  
  android:id="@+id/lblx"  
  android:layout_width="wrap_content"  
  android:layout_height="wrap_content"  
  android:layout_weight="1"  
  android:text="lblx"  
  android:textAlignment="center" />  
  
 <TextView  
  android:id="@+id/lbly"  
  android:layout_width="wrap_content"  
  android:layout_height="wrap_content"  
  android:layout_weight="1"  
  android:text="lbly"  
  android:textAlignment="center" />  
  
 <TextView  
  android:id="@+id/lblz"  
  android:layout_width="wrap_content"  
  android:layout_height="wrap_content"  
  android:layout_weight="1"  
  android:text="lblz"  
  android:textAlignment="center" />  
 </LinearLayout>  
  
 <Button  
  android:id="@+id/changeTextButton"  
  android:layout_width="wrap_content"  
  android:layout_height="wrap_content"  
  android:text="Button"  
  app:layout_constraintBottom_toBottomOf="parent"  
  app:layout_constraintEnd_toEndOf="parent"  
  app:layout_constraintStart_toStartOf="parent"  
  app:layout_constraintTop_toTopOf="parent"  
  app:layout_constraintVertical_bias="0.95" />  
  
 <TextView  
  android:id="@+id/textHint"  
  android:layout_width="wrap_content"  
  android:layout_height="wrap_content"  
  android:text="Un petit pas pour l'homme, un grand pas pour ma compréhension d'Android."  
  android:textAlignment="center"  
  app:layout_constraintBottom_toBottomOf="parent"  
  app:layout_constraintEnd_toEndOf="parent"  
  app:layout_constraintStart_toStartOf="parent"  
  app:layout_constraintTop_toTopOf="parent"  
  app:layout_constraintVertical_bias="0.05" />  
</androidx.constraintlayout.widget.ConstraintLayout>
```
### Pour attendre les autres (2 sondes)
Lire les données de 2 capteurs avec votre application (Proximité et accéléromètre?) et les afficher.
Note : pour savoir à quel capteur est associée une valeur reçue, on peut le demander via :
event.sensor.getType()

```

package com.works.a2_days;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.graphics.Color;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListView;
import android.widget.Toast;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {

    EditText txtData;
    Button btnEkle;
    ListView listView;
    ArrayList<String> list = new ArrayList<>();
    ArrayAdapter<String> adapter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        txtData = findViewById(R.id.txtData);
        btnEkle = findViewById(R.id.btnEkle);
        listView = findViewById(R.id.listView);
        btnEkle.setOnClickListener(btnEkleClick);

        dataResult();
        adapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, list);
        listView.setAdapter(adapter);
        listView.setOnItemClickListener(listClick);
        listView.setOnItemLongClickListener(listLongClick);

    }

    View.OnClickListener btnEkleClick = new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            String dt = txtData.getText().toString().trim();
            list.add(dt); // list içerisine datayı ekle.
            adapter.notifyDataSetChanged();
            txtData.setText(""); // Edittext içerisini temizle
        }
    };


    AdapterView.OnItemClickListener listClick = new AdapterView.OnItemClickListener() {
        @Override
        public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
            view.setBackgroundColor(Color.RED);
            String itemData = list.get(position);
            Toast.makeText(MainActivity.this, "Item Click : " + itemData, Toast.LENGTH_SHORT).show();

            Intent i = new Intent(MainActivity.this, Detail.class);
            i.putExtra("dataKey", itemData);
            startActivity(i);
        }
    };


    AdapterView.OnItemLongClickListener listLongClick = new AdapterView.OnItemLongClickListener() {
        @Override
        public boolean onItemLongClick(AdapterView<?> parent, View view, int position, long id) {
            /*
            view.setBackgroundColor(Color.RED);
            try {
                Thread.sleep(1500);
            }catch (Exception ex) {}
            Log.d("Uzun tıklandı", ""+position);
            view.setBackgroundColor(Color.WHITE);
            */

            list.remove(position);
            adapter.notifyDataSetChanged();
            view.setBackgroundColor(Color.WHITE);
            return true;
        }
    };



    public void dataResult() {
        list.add("İstanbul");
        list.add("Ankara");
        list.add("Bursa");
        list.add("Adana");
        list.add("İzmir");
        list.add("Gaziantep");
        list.add("Trabzon");
        list.add("Manisa");
        list.add("Samsun");
        list.add("Eskişehir");
        list.add("Van");
    }


}



```

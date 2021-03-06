#RandRoidGrid
Android UI layout the reprenste the view in random boxes.

There there 4 types of boxes that may appear in the layout in different random orders:
- Big Squar: (2 units x 2 units).
- Small Squar: (1 unit x 1 unit).
- Vertical Rectangle: (1 unit x 2 units).
- Horizintal Rectangle: (2 units x 1 unit).


NOTE: 1 unit equals to 25% of the screen width.

These shapes are order besdies each other to form one row in the grid-the row is 4 units(width)x 2 units(height).
You can insert any view (TextView, Button, ImageView ..etc) inside each box.

#Screenshots
Check out these 3 patterens (from more than 90 patterns available!)

![screenshot 1](https://cloud.githubusercontent.com/assets/1500868/4694957/315b3ee6-57de-11e4-947c-dee3b9c16774.png)
![screenshot 2](https://cloud.githubusercontent.com/assets/1500868/4694959/3afdd7f6-57de-11e4-8950-341ec85e6468.png)
![screenshot 3](https://cloud.githubusercontent.com/assets/1500868/4694961/41f52ee2-57de-11e4-9dc3-5fa49b2d2170.png)

 

#Getting Started
### 1. Download AndroidRandomGridLibrary
After you download the library project, import the project into your Eclpise WorkSpace.

### 2. Create New Android Application
After you create a new android project, you need to include the library in you project by:
Right click your project > choose properties > Choose Adnroid > Add Libray > Choose AndroidRandomGridLibrary Project.

### 3.Create Project Classes
Inside the boxes of the Grid we can display any view of group of views, in this example we will display a view that has only one text, to acheive this we need to create a class that will wrap the view component and the adapter that will map our data into views inside our grid.

**Item.java**
This class represents the data to be shown inside the grid cells.
```
public class Item {
	String title;
}
```

**MyAdapter.java**
This class which with transform the list of data into views (cells) inside the RandoGrid view.
```
import java.util.ArrayList;
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ArrayAdapter;
import android.widget.TextView;

import com.example.android500pxlayoutexample.R;

public class MyAdapter extends ArrayAdapter<String> {
	private final Context context;
	private final ArrayList<String> values;

	public MyAdapter(Context context, ArrayList<String> values) {
		super(context, R.layout.row_item, values);
		this.context = context;
		this.values = values;
	}

	@Override
	public View getView(int position, View convertView, ViewGroup parent) {

		LayoutInflater inflater = (LayoutInflater) context
				.getSystemService(Context.LAYOUT_INFLATER_SERVICE);

		View rowView = inflater.inflate(R.layout.row_item, parent, false);
		TextView tv = (TextView) rowView.findViewById(R.id.tvTitle);
		tv.setText(String.valueOf(values.get(position)));

		return rowView;
	}
}
```
**MainActivity.java** 
This class will pass the list of data into ```MyAdapter``` to display it in the grid:

1- Create instance of the RandomGrid
```
mRandomGrid = new RandomGrid();
```

2- Get the Layout from the xml that will hold the RandoGrid
```
LinearLayout mLayout = (LinearLayout) findViewById(R.id.lytBoard);
```

3-Create an list that contains the data, here we are using a dummy data demo purposes.
```
ArrayList<String> mValues = new ArrayList<String>();
   for (int i = 0; i < 20; i++) {
	mValues.add(String.valueOf(i + 1));
}
```

4- Create an adapter and pass list of data into it:
```
MyAdapter mAdapater = new MyAdapter(getApplicationContext(), mValues);
```

5- Set that adapter containing data into the randoGrid
```
mRandomGrid.setAdapter(mAdapater, mValues);
```

6- Display the RandoGrid view.
```
mRandomGrid.show(mLayout, this);
```

For the xml layout, we have 2, one fot the cell layout which in our example contains only one text, and the other is for the main activity layout:

1- activity_main.xml:
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity" >

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent" >

        <LinearLayout
            android:id="@+id/lytBoard"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical"
            tools:context=".MainActivity" >
        </LinearLayout>
    </ScrollView>

</LinearLayout>
```

2- row_item.xml
```
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity" >

    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_margin="1dp"
        android:background="#000" >

        <TextView
            android:id="@+id/tvTitle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:text="Small Text"
            android:textAppearance="?android:attr/textAppearanceSmall"
            android:textColor="#fff" />
    </FrameLayout>

</RelativeLayout>
```
#TODO

1- Instead of randomly choose the grid patterns, allow the ability to explicitly choose specific pattern.

2- Allow to distribute the content according the size of the boxes in the grid.


#License
```
Copyright (c) 2014 Adham Enaya

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

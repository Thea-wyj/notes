# Android原生开发



## 组件

### TextView

```xml
<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/fight"
    android:singleLine="true"
    android:textSize="37sp"
    android:textColor="#E16844BD"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintLeft_toLeftOf="parent"
    app:layout_constraintRight_toRightOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```

效果：

![image-20210319204002735](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210319204002735.png)

### EditText

```xml
<EditText
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:id="@+id/name"
    android:drawableLeft="@android:drawable/ic_menu_more"
    android:hint="请输入名称"
    />
<EditText
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:drawableLeft="@mipmap/pwd"
    android:hint="请输入密码"
    android:inputType="textPassword"
    />
<EditText
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:hint="请输入数字"
    android:inputType="number"
    />
<EditText
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:hint="请输入内容"
    android:lines="5"
    />
```

效果：

![image-20210319211143220](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210319211143220.png)

### Button

```xml
<Button
    android:id="@+id/button1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="按钮1" />
<Button
    android:layout_marginLeft="8dp"
    android:id="@+id/button2"
    android:layout_toRightOf="@id/button1"
    android:onClick="myClick"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="按钮2" />
```

点击事件

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //用内部类实现点击事件
        Button button = findViewById(R.id.button1);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(MainActivity.this,"单击按钮1",Toast.LENGTH_SHORT).show();
            }
        });
    }
    //用onClick属性实现点击事件
    public void  myClick(View view) {
        Toast.makeText(MainActivity.this,"单击按钮2",Toast.LENGTH_LONG).show();
    }
}
```

### ImageButton

```xml
<ImageButton
    android:background="#0000"
    android:layout_width="60dp"
    android:layout_height="40dp"
    android:src="@mipmap/bg"/>
<TextView
    android:layout_margin="12dp"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textColor="#fff"
    android:text="登录"/>
```

效果

![image-20210319214842513](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210319214842513.png)

### RadioButoon

```xml
<RadioGroup
    android:id="@+id/sex"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content">
    <RadioButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="男"/>
    <RadioButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="女"/>
    <RadioButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="保密"/>
</RadioGroup>
<Button
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:id="@+id/login"
    android:text="登录"/>
```

获取选项

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        RadioGroup radioGroup = findViewById(R.id.sex);
        radioGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(RadioGroup group, int checkedId) {
                RadioButton radioButton = findViewById(checkedId);
                Toast.makeText(MainActivity.this,radioButton.getText(),Toast.LENGTH_SHORT).show();
            }
        });
        Button button = findViewById(R.id.login);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                for(int i = 0; i< radioGroup.getChildCount(); i++) {
                    RadioButton r = (RadioButton) radioGroup.getChildAt(i);
                    if(r.isChecked()) {
                        Toast.makeText(MainActivity.this,r.getText(),Toast.LENGTH_SHORT).show();
                    }
                }
            }
        });
    }
}
```

实现效果：

![image-20210319220748561](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210319220748561.png)

### CheckBox

```xml
<CheckBox
    android:id="@+id/check1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="体育"/>
<CheckBox
    android:id="@+id/check2"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:checked="true"
    android:text="音乐"/>
<CheckBox
    android:id="@+id/check3"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="美术"/>
<CheckBox
    android:id="@+id/check4"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="编程"/>
```

效果

![image-20210320113708099](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210320113708099.png)

### DatePicker

```xml
<DatePicker
    android:id="@+id/date"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
```

回显选择内容

```java
public class MainActivity extends AppCompatActivity {
    int year,month,day;
    DatePicker datePicker;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        datePicker = findViewById(R.id.date);
        Calendar calendar = Calendar.getInstance();
        year = calendar.get(Calendar.YEAR);
        month = calendar.get(Calendar.MONTH);
        day = calendar.get(Calendar.DAY_OF_MONTH);
        datePicker.init(year, month, day, new DatePicker.OnDateChangedListener() {
            @Override
            public void onDateChanged(DatePicker view, int year, int monthOfYear, int dayOfMonth) {
                MainActivity.this.year = year;
                MainActivity.this.month = monthOfYear;
                MainActivity.this.day = dayOfMonth;
                show(year,monthOfYear,dayOfMonth);
            }
        });
    }
    private  void show(int y,int m,int d) {
        String str = year + "年" + (month + 1) + "月" + day + "日";
        Toast.makeText(MainActivity.this,str,Toast.LENGTH_SHORT).show();
    }
}
```

效果：

![image-20210320115203216](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210320115203216.png)

### TimePicker

```xml
<TimePicker
    android:id="@+id/time"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
```

显示时间：

```java
public class MainActivity extends AppCompatActivity {
    int hour,minute;
    TimePicker timePicker;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        timePicker = findViewById(R.id.time);
        timePicker.setOnTimeChangedListener(new TimePicker.OnTimeChangedListener() {
            @Override
            public void onTimeChanged(TimePicker view, int hourOfDay, int minute) {
                MainActivity.this.hour = hourOfDay;
                MainActivity.this.minute = minute;
                Toast.makeText(MainActivity.this,"现在时间：" + hourOfDay + "时" + minute + "分",Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

显示效果：

![image-20210320141723616](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210320141723616.png)

### Chronometer

```xml
<Chronometer
    android:id="@+id/chronometer"
    android:format="已用时间：%s"
    android:textColor="#FF9800"
    android:layout_alignParentRight="true"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
```

开始计时

```java
public class MainActivity extends AppCompatActivity {
    Chronometer chronometer;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        chronometer = findViewById(R.id.chronometer);
        chronometer.setBase(SystemClock.elapsedRealtime());
        chronometer.start();
        chronometer.setOnChronometerTickListener(new Chronometer.OnChronometerTickListener() {
            @Override
            public void onChronometerTick(Chronometer chronometer) {
                if(SystemClock.elapsedRealtime() - chronometer.getBase() >= 6000) {
                    Toast.makeText(MainActivity.this,"时间到",Toast.LENGTH_SHORT).show();
                    chronometer.stop();
                }
            }
        });
    }
}
```

显示效果

![image-20210320142859146](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210320142859146.png)

![image-20210320142907778](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210320142907778.png)

### ProgressBar

```xml
<ProgressBar
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

<ProgressBar
    style="?android:attr/progressBarStyleHorizontal"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:max="100"
    android:progress="30" />

<ProgressBar
    android:id="@+id/progressBar"
    style="@android:style/Widget.ProgressBar.Horizontal"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:max="100" />
```

显示

```java
public class MainActivity extends AppCompatActivity {
    private ProgressBar progressBar;
    private int data = 0;
    private Handler mHandler;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        progressBar = findViewById(R.id.progressBar);
        mHandler = new Handler() {
            @Override
            public void handleMessage(@NonNull Message msg) {
                if(msg.what == 0x111) {
                    progressBar.setProgress(data);
                } else {
                    Toast.makeText(MainActivity.this,"耗时操作已完成",Toast.LENGTH_SHORT).show();
                    progressBar.setVisibility(View.GONE);
                }
            }
        };
        new Thread(new Runnable() {
            @Override
            public void run() {
                while (true) {
                    data = doWork();
                    Message m = new Message();
                    if(data < 100) {
                        m.what = 0x111;
                        mHandler.sendMessage(m);
                    } else {
                        m.what = 0x110;
                        mHandler.sendMessage(m);
                        break;
                    }
                }
            }
            private  int doWork() {
                data += Math.random()*10;
                try {
                    Thread.sleep(200);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                return  data;
            }
        }).start();
    }
}
```

效果

![image-20210320152731809](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210320152731809.png)

### SeekBar

```xml
<SeekBar
    android:id="@+id/seekBar"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:max="10"
    android:progress="5"
    android:thumb="@drawable/peach"
    />
```

展示

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        SeekBar seekBar = findViewById(R.id.seekBar);
        seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
            @Override
            public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
                Toast.makeText(MainActivity.this, "进度改变" + progress, Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onStartTrackingTouch(SeekBar seekBar) {
                Toast.makeText(MainActivity.this, "开始触摸", Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onStopTrackingTouch(SeekBar seekBar) {
                Toast.makeText(MainActivity.this, "结束触摸", Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

显示效果

![image-20210320161043449](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210320161043449.png)

### RatingBar

```xml
<!--半颗变化 设置颗数-->
    <RatingBar
        android:id="@+id/ratingBar"
        android:numStars="6"
        android:rating="2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
<!--    单颗变化-->
    <RatingBar
        android:numStars="5"
        android:rating="1"
        android:stepSize="1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
<!--    不可修改-->
    <RatingBar
        android:numStars="5"
        android:rating="1"
        android:isIndicator="true"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
```

获得星星数

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        RatingBar ratingBar = findViewById(R.id.ratingBar);
        ratingBar.setOnRatingBarChangeListener(new RatingBar.OnRatingBarChangeListener() {
            @Override
            public void onRatingChanged(RatingBar ratingBar, float rating, boolean fromUser) {
                Toast.makeText(MainActivity.this, "当前评分" + String.valueOf(ratingBar.getProgress()), Toast.LENGTH_SHORT).show();
            }
        });
        Toast.makeText(this, "默认评分" + String.valueOf(ratingBar.getRating()), Toast.LENGTH_SHORT).show();
        Toast.makeText(this, "单次评分" + String.valueOf(ratingBar.getStepSize()), Toast.LENGTH_SHORT).show();
        Toast.makeText(this, "当前评分" + String.valueOf(ratingBar.getProgress()), Toast.LENGTH_SHORT).show();
    }
}
```

显示效果

![image-20210320163831229](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210320163831229.png)

### ImageView

```xml
<ImageView
    android:id="@+id/image"
    android:layout_width="220dp"
    android:layout_height="100dp"
    android:scaleType="fitStart"
    android:src="@drawable/bg"
    />
<ImageView
    android:id="@+id/image2"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:background="#ff0000"
    android:adjustViewBounds="true"
    android:maxWidth="90dp"
    android:maxHeight="90dp"
    android:src="@drawable/bg"
    />
<ImageView
    android:id="@+id/image3"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:adjustViewBounds="true"
    android:maxWidth="90dp"
    android:maxHeight="90dp"
    android:src="@drawable/bg"
    app:tint="#77ff0000" />
```

显示效果

![image-20210320210948294](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210320210948294.png)

### ImageSwitcher

```xml
<ImageSwitcher
    android:id="@+id/imageSwitcher"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    />
```

淡入淡出切换效果

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        ImageSwitcher imageSwitcher = findViewById(R.id.imageSwitcher);
        imageSwitcher.setOutAnimation(AnimationUtils.loadAnimation(MainActivity.this, android.R.anim.fade_out));
        imageSwitcher.setInAnimation(AnimationUtils.loadAnimation(MainActivity.this, android.R.anim.fade_in));
        imageSwitcher.setFactory(() -> {
            ImageView imageView = new ImageView(MainActivity.this);
            imageView.setImageResource(R.drawable.bg1);
            return imageView;
        });
        imageSwitcher.setOnClickListener(v -> ((ImageSwitcher)v).setImageResource(R.drawable.bg2));
    }
}
```

滑动查看手机相册实例

```java
public class MainActivity extends AppCompatActivity {
    private int[] pics = new int[]{R.drawable.bg1,R.drawable.bg2,R.drawable.bg3,R.drawable.bg4};
    private ImageSwitcher imageSwitcher;
    private int index;
    private float touchDownX;
    private float touchUpX;
    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        imageSwitcher = findViewById(R.id.imageSwitcher);
        imageSwitcher.setFactory(() -> {
            ImageView imageView = new ImageView(MainActivity.this);
            imageView.setImageResource(pics[index]);
            return imageView;
        });
        imageSwitcher.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View v, MotionEvent event) {
                if (event.getAction() == MotionEvent.ACTION_DOWN) {
                    touchDownX = event.getX();
                    return true;
                } else if(event.getAction() == MotionEvent.ACTION_UP) {
                    touchUpX = event.getX();
                    if((touchUpX - touchDownX) > 100) {
                        index = index==0? pics.length-1:index-1;
                        imageSwitcher.setInAnimation(AnimationUtils.loadAnimation(MainActivity.this, android.R.anim.slide_in_left));
                        imageSwitcher.setOutAnimation(AnimationUtils.loadAnimation(MainActivity.this, android.R.anim.slide_out_right));
                        imageSwitcher.setImageResource(pics[index]);
                    } else if((touchDownX - touchUpX) > 100) {
                        index = index==pics.length - 1? 0:index+1;
                        imageSwitcher.setInAnimation(AnimationUtils.loadAnimation(MainActivity.this, android.R.anim.fade_in));
                        imageSwitcher.setOutAnimation(AnimationUtils.loadAnimation(MainActivity.this, android.R.anim.fade_out));
                        imageSwitcher.setImageResource(pics[index]);
                    }
                    return true;
                }
                return false;
            };
        });
    }
}
```

### GridView

```xml
<GridView
    android:id="@+id/gridView"
    android:numColumns="auto_fit"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
</GridView>
```

用xml文件实现适配器

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <ImageView
        android:id="@+id/image"
        android:scaleType="fitXY"
        android:layout_width="100dp"
        android:layout_height="75dp"/>

</LinearLayout>
```

实现图片资源渲染

```java
public class MainActivity extends AppCompatActivity {
    private int[] pics = new int[]{R.drawable.bg1,R.drawable.bg2,R.drawable.bg3,R.drawable.bg4};
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        GridView gridView = findViewById(R.id.gridView);
        gridView.setAdapter(new ImageAdapter(this));
//        通过引用xml文件实现适配器
//        GridView gridView = findViewById(R.id.gridView);
//        List<Map<String,Object>> listItem = new ArrayList<Map<String,Object>>();
//        for (int i = 0; i<pics.length;i++) {
//            Map<String,Object> map = new HashMap<String, Object>();
//            map.put("image",pics[i]);
//            listItem.add(map);
//        }
//        SimpleAdapter simpleAdapter = new SimpleAdapter(this,listItem,R.layout.cell,new String[]{"image"},new int[]{R.id.image});
//        gridView.setAdapter(simpleAdapter);
    }
    public class ImageAdapter extends BaseAdapter{
        private Context context;

        public ImageAdapter(Context context) {
            this.context = context;
        }

        @Override
        public int getCount() {
            return pics.length;
        }

        @Override
        public Object getItem(int position) {
            return null;
        }

        @Override
        public long getItemId(int position) {
            return 0;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {
            ImageView imageView;
            if(convertView == null) {
                imageView = new ImageView(context);
                imageView.setLayoutParams(new ViewGroup.LayoutParams(500,250));
                imageView.setScaleType(ImageView.ScaleType.CENTER_CROP);
            } else {
                imageView = (ImageView) convertView;
            }
            imageView.setImageResource(pics[position]);
            return imageView;
        }
    }
}
```

### Spinner

1.根据数组资源文件加载

```xml
<Spinner
    android:id="@+id/spinner"
    android:entries="@array/ctype"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content">

</Spinner>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="ctype">
        <item>全部</item>
        <item>电影</item>
        <item>图书</item>
        <item>游戏</item>
    </string-array>
</resources>
```

2.根据适配器加载

```xml
<Spinner
    android:id="@+id/spinner"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content">

</Spinner>
```

绑定适配器并获取值

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        String[] ctype = new String[] {"全部","美术","音乐","体育"};
        ArrayAdapter<String> arrayAdapter = new ArrayAdapter<String>(this, android.R.layout.simple_spinner_item,ctype);
        arrayAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        Spinner spinner = findViewById(R.id.spinner);
        spinner.setAdapter(arrayAdapter);
        spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                Toast.makeText(MainActivity.this,"选中了"+ctype[position],Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onNothingSelected(AdapterView<?> parent) {
                
            }
        });
    }
}
```

显示效果

![image-20210321094602982](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321094602982.png)

### ListView

通过数组资源文件设置

```xml
<ListView
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:entries="@array/ctype">
</ListView>
```

通过适配器来设置

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        String[] ctype = new String[]{"全部","美术","音乐","体育"};
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1,ctype);
        ListView listView = findViewById(R.id.listView);
        listView.setAdapter(adapter);
    }
}
```

根据适配器显示图文列表

```xml
<ListView
    android:id="@+id/listView"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">
</ListView>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:padding="3dp"
    android:orientation="horizontal"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <ImageView
        android:id="@+id/image"
        android:scaleType="fitStart"
        android:layout_width="250dp"
        android:layout_height="125dp"/>

    <TextView
        android:id="@+id/name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"/>

</LinearLayout>
```

装配适配器并设计点击显示内容事件、

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        int[] imageId = new int[]{R.drawable.bg1, R.drawable.bg2, R.drawable.bg3, R.drawable.bg4};
        String[] name = new String[]{"第一个", "第二个", "第三个", "第四个"};
        List<Map<String, Object>> viewList = new ArrayList<Map<String, Object>>();
        for (int i = 0; i < imageId.length; i++) {
            Map<String, Object> map = new HashMap<String, Object>();
            map.put("image", imageId[i]);
            map.put("name", name[i]);
            viewList.add(map);
        }
        SimpleAdapter adapter = new SimpleAdapter(this, viewList, R.layout.item, new String[]{"name", "image"}, new int[]{R.id.name, R.id.image});
        ListView listView = findViewById(R.id.listView);
        listView.setAdapter(adapter);
        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                Map<String, Object> map = (Map<String, Object>) parent.getItemAtPosition((position));
                Toast.makeText(MainActivity.this, map.get("name").toString(), Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

显示效果

![image-20210321101618437](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321101618437.png)

在资源文件中添加滚动视图

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
<!--    一个滚动视图只能放一个组件！！-->
<!--&lt;!&ndash;垂直滚动&ndash;&gt;-->
<!--    <ScrollView-->
<!--        android:layout_width="match_parent"-->
<!--        android:layout_height="wrap_content">-->
<!--        <TextView-->
<!--            android:text="@string/content"-->
<!--            android:layout_width="match_parent"-->
<!--            android:layout_height="match_parent"-->
<!--            android:textSize="40sp"></TextView>-->
<!--    </ScrollView>-->
<!--    水平滚动-->
    <HorizontalScrollView
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <LinearLayout
            android:orientation="vertical"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content">
            <TextView
                android:text="@string/content"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:textSize="20sp"></TextView>
            <TextView
                android:text="@string/content"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:textSize="20sp"></TextView>
        </LinearLayout>
    </HorizontalScrollView>

</RelativeLayout>
```

在java文件中显示滚动视图

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        LinearLayout linearLayout = findViewById(R.id.linear);
        LinearLayout linearLayout1 = new LinearLayout(MainActivity.this);
        linearLayout1.setOrientation(LinearLayout.VERTICAL);
        ScrollView scrollView = new ScrollView(MainActivity.this);
        linearLayout.addView(scrollView);
        scrollView.addView(linearLayout1);
        ImageView imageView = new ImageView(MainActivity.this);
        imageView.setImageResource(R.drawable.bg);
        imageView.setScaleType(ImageView.ScaleType.FIT_START);
        linearLayout1.addView(imageView);
        TextView textView = new TextView(MainActivity.this);
        textView.setText(R.string.content);
        linearLayout1.addView(textView);

    }
}
```

activiMain.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:orientation="vertical"
    android:padding="16dp"
    android:id="@+id/linear"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

</LinearLayout>
```

显示效果

![image-20210321104424523](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321104424523.png)

### TabHost

```xml
<?xml version="1.0" encoding="utf-8"?>
<TabHost xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@android:id/tabhost"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

   <LinearLayout
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical">
       <TabWidget
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:id="@android:id/tabs"></TabWidget>
       <FrameLayout
           android:id="@android:id/tabcontent"
           android:layout_width="match_parent"
           android:layout_height="match_parent">

       </FrameLayout>
   </LinearLayout>

</TabHost>
```

tab1

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:padding="16dp"
    android:id="@+id/tab1"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="选项1"/>
</LinearLayout>
```

tab2

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:padding="16dp"
    android:id="@+id/tab2"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="选项2"/>
</LinearLayout>
```

添加tab切换

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        TabHost tabHost = findViewById(android.R.id.tabhost);
        tabHost.setup();
        LayoutInflater layoutInflater = LayoutInflater.from(this);
        layoutInflater.inflate(R.layout.tab1,tabHost.getTabContentView());
        layoutInflater.inflate(R.layout.tab2,tabHost.getTabContentView());
        tabHost.addTab(tabHost.newTabSpec("tab1").setIndicator("精选表情").setContent(R.id.tab1));
        tabHost.addTab(tabHost.newTabSpec("tab2").setIndicator("投稿表情").setContent(R.id.tab2));
    }
}
```

显示效果

![image-20210321105756881](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321105756881.png)

### Activity的四种状态

![image-20210321140325480](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321140325480.png)

![image-20210321140405512](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321140405512.png)

在当前页面启动另一个activity

```java
Button button = findViewById(R.id.mainButton);
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Intent intent = new Intent(MainActivity.this,MyActivity.class);
        startActivity(intent);
    }
});
```

在本页面关闭activity（返回）

```java
Button button = findViewById(R.id.myButton2);
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        finish();
    }
});
```

刷新当前Activity（当Activity继承自AppCompatActivity时会有问题）

![image-20210321143831627](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321143831627.png)

```java
Button button2 = findViewById(R.id.mainButton2);
button2.setOnClickListener(new View.OnClickListener() {
    @Override
    public voi     d onClick(View v) {
        onCreate(null);
    }
});
```

### Bundle实现跳转传值实例

mainActivity

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:padding="16dp"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/name"
        android:hint="请输入姓名"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
    <EditText
        android:id="@+id/phone"
        android:hint="请输入联系方式"
        android:inputType="number"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
    <EditText
        android:hint="请输入地址"
        android:id="@+id/location"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
    <Button
        android:id="@+id/submit"
        android:text="保存地址"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

</LinearLayout>
```

locationActivity

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp"
    tools:context=".LocationShow">

    <TextView
        android:id="@+id/name"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <TextView
        android:id="@+id/phone"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <TextView
        android:id="@+id/location"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />


</LinearLayout>
```

传值

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button button = findViewById(R.id.submit);
        button.setOnClickListener(v -> {
            String name = ((EditText) findViewById(R.id.name)).getText().toString();
            String phone = ((EditText) findViewById(R.id.phone)).getText().toString();
            String location = ((EditText) findViewById(R.id.location)).getText().toString();
            if (name.equals("") || phone.equals("") || location.equals("")) {
                Toast.makeText(MainActivity.this, "请将地址输入完整", Toast.LENGTH_SHORT).show();
            } else {
                Intent intent = new Intent(MainActivity.this,LocationShow.class);
                Bundle bundle = new Bundle();
                bundle.putCharSequence("name",name);
                bundle.putCharSequence("phone",phone);
                bundle.putCharSequence("location",location);
                intent.putExtras(bundle);
                startActivity(intent);
            }
        });
    }
}
```

获取值

```java
public class LocationShow extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_location_show);
        Intent intent = getIntent();
        Bundle bundle = intent.getExtras();
        ((TextView)findViewById(R.id.name)).setText(bundle.getString("name"));
        ((TextView)findViewById(R.id.phone)).setText(bundle.getString("phone"));
        ((TextView)findViewById(R.id.location)).setText(bundle.getString("location"));
    }
}
```

效果展示

![image-20210321153823992](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321153823992.png)

![image-20210321153835690](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321153835690.png)

`傻逼错误：EditText的获取文本操作只能在监听事件中获取`

### 调用另外Activity返回结果StartActivityForResult()

mainActivity

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:padding="16dp"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    <ImageView
        android:id="@+id/profile"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:src="@drawable/profile"/>
    <Button
        android:id="@+id/change"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:text="更换头像"/>


</LinearLayout>
```

另一个图片列表Activity

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:padding="16dp"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <GridView
        android:id="@+id/gridView"
        android:numColumns="auto_fit"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
    </GridView>

</RelativeLayout>
```

主页面跳转

```java
public class MainActivity extends Activity {
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if(requestCode == 0x11 && resultCode == 0x11) {
            Bundle bundle = data.getExtras();
            ImageView imageView = findViewById(R.id.profile);
            imageView.setImageResource(bundle.getInt("imageId"));

        }
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button button = findViewById(R.id.change);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainActivity.this,ImagListActivity.class);
                startActivityForResult(intent,0x11);
            }
        });
    }
}
```

跳转后获取值并返回

```java
public class ImagListActivity extends AppCompatActivity {
    private int[] pics = new int[]{R.drawable.bg1, R.drawable.bg2, R.drawable.bg3, R.drawable.bg4};

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_imag_list);
        //        通过引用xml文件实现适配器
        GridView gridView = findViewById(R.id.gridView);
        List<Map<String, Object>> listItem = new ArrayList<Map<String, Object>>();
        for (int i = 0; i < pics.length; i++) {
            Map<String, Object> map = new HashMap<String, Object>();
            map.put("image", pics[i]);
            listItem.add(map);
        }
        SimpleAdapter simpleAdapter = new SimpleAdapter(this, listItem, R.layout.cell, new String[]{"image"}, new int[]{R.id.image});
        gridView.setAdapter(simpleAdapter);
        gridView.setOnItemClickListener((parent, view, position, id) -> {
            Intent intent = getIntent();
            Bundle bundle = new Bundle();
            bundle.putInt("imageId",pics[position]);
            intent.putExtras(bundle);
            setResult(0x11,intent);
            finish();
        });

    }
}
```

显示效果

![image-20210321162153242](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321162153242.png)

![image-20210321162204166](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210321162204166.png)

### Fragment

创建

```java
public class DetailFragment extends Fragment {
    @Nullable
    @Override
    public View onCreateView(@NonNull @org.jetbrains.annotations.NotNull LayoutInflater inflater, @Nullable @org.jetbrains.annotations.Nullable ViewGroup container, @Nullable @org.jetbrains.annotations.Nullable Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment_detail,container,false);
        return super.onCreateView(inflater, container, savedInstanceState);
    }
}
```

添加Fragment到Activity中

1.通过布局文件

```xml
<fragment
    android:id="@+id/list"
    android:name="com.example.fragmentdemo.ListFragment"
    android:layout_width="wrap_content"
    android:layout_height="match_parent"
    android:layout_weight="1" />

<fragment
    android:id="@+id/detail"
    android:name="com.example.fragmentdemo.DetailFragment"
    android:layout_width="wrap_content"
    android:layout_height="match_parent"
    android:layout_weight="2" />
```

在Activity运行时添加

```java
DetailFragment detailFragment = new DetailFragment();
FragmentTransaction fragmentTransaction = getFragmentManager().beginTransaction();
fragmentTransaction.add(R.id.frameLayOut,detailFragment);
fragmentTransaction.commit();
```

### Fragment实现tab切换

mainActivity

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
<!--解决fragment重叠问题-->
<!--    <fragment-->
<!--        android:id="@+id/fragment"-->
<!--        android:layout_width="match_parent"-->
<!--        android:layout_height="match_parent"-->
<!--        android:name="com.example.wechatdemo.WeChat_Fragment"/>-->
    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/layout"/>
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:layout_alignParentBottom="true"
        android:orientation="horizontal">
        <ImageView
            android:id="@+id/tab1"
            android:background="#78B761"
            android:layout_width="0dp"
            android:layout_height="50dp"
            android:layout_weight="1"
            android:src="@android:drawable/ic_dialog_info"
            />
        <ImageView
            android:id="@+id/tab2"
            android:background="#78B761"
            android:layout_width="0dp"
            android:layout_height="50dp"
            android:layout_weight="1"
            android:src="@android:drawable/ic_menu_today"
            />
        <ImageView
            android:id="@+id/tab3"
            android:background="#78B761"
            android:layout_width="0dp"
            android:layout_height="50dp"
            android:layout_weight="1"
            android:src="@android:drawable/ic_menu_search"
            />
        <ImageView
            android:id="@+id/tab4"
            android:background="#78B761"
            android:layout_width="0dp"
            android:layout_height="50dp"
            android:layout_weight="1"
            android:src="@android:drawable/ic_menu_myplaces"
            />
    </LinearLayout>

</RelativeLayout>
```

fragment切换

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        FragmentManager fragmentManager = getFragmentManager();
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
        fragmentTransaction.add(R.id.layout,new WeChat_Fragment());
        fragmentTransaction.commit();
        ImageView imageView1 = findViewById(R.id.tab1);
        ImageView imageView2 = findViewById(R.id.tab2);
        ImageView imageView3 = findViewById(R.id.tab3);
        ImageView imageView4 = findViewById(R.id.tab4);
        imageView1.setOnClickListener(l);
        imageView2.setOnClickListener(l);
        imageView3.setOnClickListener(l);
        imageView4.setOnClickListener(l);
    }

    View.OnClickListener l = v -> {
        FragmentManager fragmentManager = getFragmentManager();
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
        Fragment fragment = null;
        switch (v.getId()) {
            case R.id.tab1:
                fragment = new WeChat_Fragment();
                break;
                case R.id.tab2:
                fragment = new Message_Fragment();
                break;
                case R.id.tab3:
                fragment = new Find_Fragment();
                break;
                case R.id.tab4:
                fragment = new Me_Fragment();
                break;
            default:break;
        }
        fragmentTransaction.replace(R.id.layout,fragment);
        fragmentTransaction.commit();
    };
}
```

显示效果：

![image-20210322121753832](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322121753832.png)

### Intent

 通过ComponentName进行传递

```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    Button button = findViewById(R.id.button);
    button.setOnClickListener(v -> {
        Intent intent = new Intent();
        ComponentName componentName = new ComponentName("com.example.intentdemo","com.example.intentdemo.DetailActivity");
        intent.setComponent(componentName);
        startActivity(intent);
    });
}
```

#### Action + Data

实例：跳转发送短信以及拨打电话页面

```xml
<ImageButton
    android:background="#00ffffff"
    android:id="@+id/phone"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/ic_phone_foreground"/>
<ImageButton
    android:background="#00ffffff"
    android:id="@+id/message"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/ic_message_foreground"/>
```

设置点击事件

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        ImageButton phone = findViewById(R.id.phone);
        ImageButton message = findViewById(R.id.message);
        phone.setOnClickListener(l);
        message.setOnClickListener(l);
    }
    View.OnClickListener l = v -> {
        Intent intent = new Intent();
        ImageButton imageButton = (ImageButton) v;
        switch (imageButton.getId()) {
            case R.id.phone:intent.setAction(intent.ACTION_DIAL);
            intent.setData(Uri.parse("tel:15128943765"));
            startActivity(intent);
            break;
            case R.id.message: intent.setAction(intent.ACTION_SENDTO);
            intent.setData(Uri.parse("smsto:15128943765"));
            intent.putExtra("sms_body","测试");
            startActivity(intent);
            break;
        }
    };
}
```

![image-20210322121714565](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322121714565.png)

#### Action + Category

1.返回系统桌面

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Intent intent = new Intent();
        Button button = findViewById(R.id.back);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent();
                intent.setAction(intent.ACTION_MAIN);
                intent.addCategory(intent.CATEGORY_HOME);
                startActivity(intent);
            }
        });
    }
}
```

#### Extras

#### Flags

```JAVA
Intent intent = new Intent(MainActivity.this,DetailActivity.class);
intent.setFlags(intent.FLAG_ACTIVITY_NO_HISTORY);
startActivity(intent);
```

#### 显示Intent

```java
Intent intent = new Intent(MainActivity.this,DetailActivity.class);
```

#### 隐式Intent

![image-20210322123228976](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322123228976.png)

跳转打开网页：

```java
goWeb.setOnClickListener(v -> {
    Intent intent = new Intent();
    intent.setAction(intent.ACTION_VIEW);
    intent.setData(Uri.parse("http://www.baidu.com"));
    startActivity(intent);
});
```

区别：

![image-20210322123918955](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322123918955.png)

#### intent过滤器

```java
Intent intent = new Intent();
intent.setAction(intent.ACTION_VIEW);
startActivity(intent);
```

```xml
<activity android:name=".ShowActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />

        <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
</activity>
```

![image-20210322125855629](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210322125855629.png)

### 基于回调的事件处理

```java
@Override
public boolean onKeyDown(int keyCode, KeyEvent event) {
    Toast.makeText(this, "按下", Toast.LENGTH_SHORT).show();
    return super.onKeyDown(keyCode, event);
}

@Override
public boolean onKeyUp(int keyCode, KeyEvent event) {
    Toast.makeText(this, "抬起", Toast.LENGTH_SHORT).show();
    return super.onKeyUp(keyCode, event);
}

@Override
public boolean onTouchEvent(MotionEvent event) {
    Toast.makeText(this, "触摸", Toast.LENGTH_SHORT).show();
    return super.onTouchEvent(event);
}
```

效果：

![image-20210322202042640](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322202042640.png)

![image-20210322202114356](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322202114356.png)

![image-20210322202009661](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322202009661.png)

### 物理按键事件处理

![image-20210322202223685](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322202223685.png)

![image-20210322202308451](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322202308451.png)

连续两次按退出键返回操作

```java
//    定义第一次按的时间
    private long exitTime = 0;
    @Override
//    定义按下按键事件
    public boolean onKeyDown(int keyCode, KeyEvent event) {
//        如果按的是返回键
        if (keyCode == KeyEvent.KEYCODE_BACK) {
            exit();
            return true;
        } else {
            Toast.makeText(this, "按下", Toast.LENGTH_SHORT).show();
        }
        return super.onKeyDown(keyCode, event);
    }
    public void exit() {
//        如果两次间隔时间不在两秒内
        if((System.currentTimeMillis() - exitTime) > 2000) {
            Toast.makeText(this, "再按一次退出程序", Toast.LENGTH_SHORT).show();
            exitTime = System.currentTimeMillis();
        } else {
//            退出程序
            finish();
            System.exit(0);
        }
    }
```

### 屏幕操作事件

#### 长按事件

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    ImageView imageView = findViewById(R.id.image);
    imageView.setOnLongClickListener(new View.OnLongClickListener() {
        @Override
        public boolean onLongClick(View v) {
            Log.i("长按","长按");
            registerForContextMenu(v);
            openContextMenu(v);
            return true;
        }
    });
}

@Override
public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
    super.onCreateContextMenu(menu, v, menuInfo);
    menu.add("收藏");
    menu.add("举报");
}
```

![image-20210322211157505](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322211157505.png)

#### 触摸事件

HatView

```java
public class HatView extends View {
    public float bitmapX;
    public float bitmapY;
    public HatView(Context context) {
        super(context);
        bitmapX = 65;
        bitmapX = 0;
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        Paint paint = new Paint();
        Bitmap bitmap = BitmapFactory.decodeResource(this.getResources(),R.drawable.hat);
        canvas.drawBitmap(bitmap,bitmapX,bitmapY,paint);
        if(bitmap.isRecycled()) {
            bitmap.recycle();
        }
    }
}
```

给帽子添加触摸事件

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //创造帽子实例
        HatView hatView = new HatView(MainActivity.this);
        hatView.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View v, MotionEvent event) {
                hatView.bitmapX = event.getX() - 80;
                hatView.bitmapY = event.getY() - 80;
                hatView.invalidate();
                return true;
            }
        });
        //将帽子添加到布局管理器中
        RelativeLayout relativeLayout = findViewById(R.id.background);
        relativeLayout.addView(hatView);
    }
}
```

显示效果：

![image-20210322213329479](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322213329479.png)

![image-20210322213556725](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210322213556725.png)

### 手势检测

通过手势检测实现左滑右滑切换图片

图片布局：

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:padding="16dp"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <ViewFlipper
        android:id="@+id/flipper"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</RelativeLayout>
```

切换事件

```java
//第一步：让MainActivity实现GestureDetector.OnGestureListener接口,并实现其所有方法
public class MainActivity extends Activity implements GestureDetector.OnGestureListener {
    Animation[] animations = new Animation[4];
    final int distance = 50;
    private int[] images = new int[]{R.drawable.img01, R.drawable.img02, R.drawable.img03, R.drawable.img04, R.drawable.img05, R.drawable.img06, R.drawable.img07, R.drawable.img08,};
    //    第二步，定义全局手势检测器
    ViewFlipper viewFlipper;
    GestureDetector detector;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        detector = new GestureDetector(MainActivity.this, this);
//        第三步，将要显示的图片加载到ViewFlipper中，并且初始化动画数组
        viewFlipper = findViewById(R.id.flipper);
        for (int i = 0; i < images.length; i++) {
            ImageView imageView = new ImageView(this);
            imageView.setImageResource(images[i]);
            viewFlipper.addView(imageView);
        }
        animations[0] = AnimationUtils.loadAnimation(this, R.anim.slide_in_left);
        animations[1] = AnimationUtils.loadAnimation(this, R.anim.slide_out_left);
        animations[2] = AnimationUtils.loadAnimation(this, R.anim.slide_in_right);
        animations[3] = AnimationUtils.loadAnimation(this, R.anim.slide_out_right);
    }

    @Override
    public boolean onDown(MotionEvent e) {
        return false;
    }

    @Override
    public void onShowPress(MotionEvent e) {

    }

    @Override
    public boolean onSingleTapUp(MotionEvent e) {
        return false;
    }

    @Override
    public boolean onScroll(MotionEvent e1, MotionEvent e2, float distanceX, float distanceY) {
        return false;
    }

    @Override
    public void onLongPress(MotionEvent e) {

    }


    @Override
    public boolean onFling(MotionEvent e1, MotionEvent e2, float velocityX, float velocityY) {
//        第四步，通过触点位置判断是向左滑还是向右滑
        if (e1.getX() - e2.getX() > distance) {
            viewFlipper.setInAnimation(animations[2]);
            viewFlipper.setOutAnimation(animations[1]);
            viewFlipper.showPrevious();
            return true;
        } else if (e2.getX() - e1.getX() > distance) {
            viewFlipper.setInAnimation(animations[0]);
            viewFlipper.setOutAnimation(animations[3]);
            viewFlipper.showNext();
            return true;
        }
        return false;
    }

    //        第五步，将Activity上的触摸事件交给GestureDetector处理
    @Override
    public boolean onTouchEvent(MotionEvent event) {
        return detector.onTouchEvent(event);
    }

    @Override
    public void onPointerCaptureChanged(boolean hasCapture) {

    }
}
```
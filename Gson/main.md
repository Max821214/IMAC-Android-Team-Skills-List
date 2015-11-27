# Gson
***
### Development Environment
* Android Studio 
### Built Environment
* �}�� Android Srudio
* �إ߷s�� project �s�� Gson

![](./project.png)

* �}�� Gson �� build.gradle(Module:app)�A�b dependencies �϶��[�J�A�ҡG
```
 dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:22.2.0'
    //compile �N��|�b���ε{�����涥�q�A�ϥΨ�o�Ө禡�w
    //�ثe�̷s����2.5
    compile 'com.google.code.gson:gson:2.5'
}
```

### The Simplest Sample
```public class MainActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //�إ�Classmate����
        Classmate classmate = new Classmate("Jerry",20,"01-123456789");
        //�إ�Gson����
        Gson gson = new Gson();
        //�NClassmate�����ഫ��Json
        String Json = gson.toJson(classmate);
        System.out.println(Json);

        //�NJson�ഫ������
        Classmate classmateJson =  gson.fromJson(Json,Classmate.class);
        System.out.println(classmateJson.getname());
        System.out.println(classmateJson.getage());
        System.out.println(classmateJson.getphone());

    }
}
//�إߦP�ǳq�T�����O
class Classmate {
    private String name;
    private int age;
    private String phone;
//�غc�l
    public Classmate(String name, int age, String phone) {
        this.name = name;
        this.age = age;
        this.phone = phone;
    }

    public String getname() {return this.name;}
    public void setName(String name){this.name=name;}
    public int getage() {return this.age;}
    public void setage(int age){this.age=age;}
    public String getphone() {return this.phone;}
    public void setphone(String phone){this.phone=phone;}
}
```
### Result
```
 {"name":"Jerry","phone":"01-123456789","age":20}
System.out�R Jerry
System.out�R 20
System.out�R 01-123456789
```




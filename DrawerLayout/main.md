#DrawerLayout

#### Development Environment
- Windows 7
- Android Studio 1.3.1

#### Built Environment
- �}�� Android Studio

- �إ߷s�� App �s�� DrawLayout

![](./picture/Workspace1_001.png)

- �}�� DrawLayout Project �� build.gradle�A�b dependencies �϶��[�J�A�ҡG

```gradle
dependencies {
    compile fileTree(include: ['*.jar'], dir: 'libs')
    // compile �N��|�b���ε{�����涥�q�A�ϥΨ�o�Ө禡�w�A�o��ϥ�appcompat-v7��23.0.1���C
    compile 'com.android.support:appcompat-v7:23.0.1'
    // compile �N��|�b���ε{�����涥�q�A�ϥΨ�o�Ө禡�w�A�o��ϥ�support-v4��23.0.1���C
    compile 'com.android.support:support-v4:23.0.1'
}
```

#### The Simplest Sample
```java
public class MainActivity extends AppCompatActivity {
    private MainLayout layout;
    private ActionBarDrawerToggle mDrawerToggle;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        initActionBar();
        initDrawerLayout();
        initDrawerList();
    }

    /***
     * �bnavigation drawer���XActionBar�A��ActionBar����^�b����{�A�åB�� App icon �i�H�Q�I��C
     */
    private void initActionBar() {
        getSupportActionBar().setDisplayHomeAsUpEnabled(true);
        getSupportActionBar().setHomeButtonEnabled(true);
    }

    /***
     * �������X�{����l�Ƴ]�w
     */
    private void initDrawerLayout() {
        setContentView(layout = new MainLayout(this));

        //�إ߰����Ĳ�o���A�䤤�|�N�����B�}�ҩM�������O���Ѽƫ��w��ActionBarDrawerToggle(�ϥ�appcompat-v7)
        mDrawerToggle = new ActionBarDrawerToggle(this, layout.drawerLayout, R.string.drawer_open, R.string.drawer_close){
            //�U���O����мg��k�A���O�O�Ұ���� onDrawerOpened ����������� onDrawerClosed�A�i�H�A�}�ҩ����������w�ʧ@�C
            @Override
            public void onDrawerClosed(View drawerView) {
                super.onDrawerClosed(drawerView);
            }

            @Override
            public void onDrawerOpened(View drawerView) {
                super.onDrawerOpened(drawerView);
            }
        };

        //�I�ssyncState(); �� ActionBar ������^�b���m�����T���u�ϥܡC
        mDrawerToggle.syncState();

        //��drawerLayout��ť�o��Ĳ�o��
        layout.drawerLayout.setDrawerListener(mDrawerToggle);
    }

    /***
     * �b����椤�HlistView�覡��ܡA�Φr��}�C�إ�adapter���listView��
     */
    private void initDrawerList() {
        String[] drawArray = this.getResources().getStringArray(R.array.items_array);
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, drawArray);
        layout.listView.setAdapter(adapter);
    }

    /***
     * ��appicon�i�H���}����檺�ʧ@
     * @param item
     * @return
     */
    @Override
    public boolean onOptionsItemSelected(MenuItem item) {

        if (mDrawerToggle.onOptionsItemSelected(item)) {
            return true;
        }
        return super.onOptionsItemSelected(item);
    }
}
```

![](./picture/Workspace1_002.png)

#### Contributors
MaxJiang

#### Troubleshooting
- �]���n�ϥΰ���檺�ܡALayoutParams �n�ϥ� DrawLayout �M�Ϊ��A�ӥB�b�ݩʤ譱���F�����e���A�ٶ��]�w����l�Ʀ�m�A��:
```java
    private ListView listView() {
        DrawerLayout.LayoutParams params = new DrawerLayout.LayoutParams(ruler.getW(60), LayoutParams.MATCH_PARENT, Gravity.LEFT);

        ListView v = new ListView(getContext());
        v.setBackgroundColor(Color.RED);
        v.setLayoutParams(params);
        return v;
    }
```
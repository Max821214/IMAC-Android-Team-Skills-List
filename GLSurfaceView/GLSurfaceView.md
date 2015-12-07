#GLSurfaceView

#### Development Environment
- Windows 7 SP1
- Android Studio 1.4

#### Built Environment
- �}�� Android Studio 

- �إ߷s�� project �s�� OpenGLSurfaceView

#### The Simplest Sample
- �ק� MainActivity 
```JAVA
public class MainActivity extends Activity {
private GLSurfaceViewLayout glSurfaceView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(glSurfaceView = new GLSurfaceView(this));

        // �]�m GLSurfaceView 
        glSurfaceView.setRenderer(new GLRenderer());
    }

    @Override
    protected void onResume() {
        super.onResume();
        glSurfaceView.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
        glSurfaceView.onPause();
    }
}
```
- �s�ؤ@�� Class �s�� GLRenderer �åB��@ GLSurfaceView.Renderer ����
```JAVA
public class GLRenderer implements GLSurfaceView.Renderer {
    // �]�w���I buffer
    private FloatBuffer verticesBuffer;
    // �]�w���� buffer
    private ShortBuffer indexBuffer;
    // �]�w����
    private float angle = 0f;

    // ���I�y��
    private float vertices[] = {
            -1.0f, -1.0f, -1.0f,  // 0
            1.0f, -1.0f, -1.0f,   // 1
            1.0f, 1.0f, -1.0f,    // 2
            -1.0f, 1.0f, -1.0f,   // 3
            -1.0f, -1.0f, 1.0f,   // 4
            1.0f, -1.0f, 1.0f,    // 5
            1.0f, 1.0f, 1.0f,     // 6
            -1.0f, 1.0f, 1.0f,    // 7
    };
    // ���I����
    private short index[] = {
            0, 4, 5,
            0, 5, 1,
            1, 5, 6,
            1, 6, 2,
            2, 6, 7,
            2, 7, 3,
            3, 7, 4,
            3, 4, 0,
            4, 7, 6,
            4, 6, 5,
            3, 0, 1,
            3, 1, 2,};

    @Override
    // ����k�]�m�@��ø�s�ɤ��`���ܪ��Ѽ�
    public void onSurfaceCreated(GL10 gl, EGLConfig config) {
        // �]�m�I���C�� ( RGBA )
        gl.glClearColor(1.0f, 0.5f, 0.0f, 0.5f);
        // �ҥΥ��ƪ������A���@�w�ݭn
        gl.glShadeModel(GL10.GL_SMOOTH);
        // �]�w�`�h buffer
        gl.glClearDepthf(1.0f);
        // �ҥβ`�h����
        gl.glEnable(GL10.GL_DEPTH_TEST);
        // ����`�״��ժ�����
        gl.glDepthFunc(GL10.GL_LEQUAL);
        // �]�w�z���ץ�
        gl.glHint(GL10.GL_PERSPECTIVE_CORRECTION_HINT, GL10.GL_NICEST);
    }

    @Override
    // ��ù�����ܤ�V�ɰ��榹��k
    public void onSurfaceChanged(GL10 gl, int width, int height) {
        // �]�w��e���e���y��
        gl.glViewport(0, 0, width, height);
        // �]�m����v�x�}
        gl.glMatrixMode(GL10.GL_PROJECTION);
        // �p��e�����e����A�H�λ��p��j������ĪG
        GLU.gluPerspective(
                gl,                             // ���Ī� GL10
                65.0f,                          // ����
                (float) width / (float) height, // ��V
                0.1f,                           // �� Z �b
                100.0f);                        // ���� Z �b
        // �]�m���ҫ��e���x�}
        gl.glMatrixMode(GL10.GL_MODELVIEW);
        // ���m�e���x�}
        gl.glLoadIdentity();
    }

    @Override
    // �w�q���ø�Ϫ��ާ@
    public void onDrawFrame(GL10 gl) {
        // �M���e���H�β`�h�w��
        gl.glClear(GL10.GL_COLOR_BUFFER_BIT | GL10.GL_DEPTH_BUFFER_BIT);
        // �]�w��e�e���x�}���ҫ��e���x�}
        gl.glMatrixMode(GL10.GL_MODELVIEW);
        // ���m�e���x�}
        gl.glLoadIdentity();
        // �]�m���� ( �q�`���|���� )
        GLU.gluLookAt(gl, 0, 0, 4, 0, 0, 0, 0, 1, 0);
        // �]�w ø�s�e�V�������I���Ǭ��f�ɰw��V
        gl.glFrontFace(GL10.GL_CCW);
        // �ҥΩ����� ( FACE )
        gl.glEnable(GL10.GL_CULL_FACE);
        // ���w������V��
        gl.glCullFace(GL10.GL_BACK);
        // �ҥγ��I buffer ���g�J�A�H�έn�ϥΪ��٬V�L�{
        gl.glEnableClientState(GL10.GL_VERTEX_ARRAY);

        // �]�w�C�� ( RGBA )
        gl.glColor4f(1f, 1f, 0f, 0f);

        // ����ߤ��� (����, X, Y, Z)
        gl.glRotatef(angle, 1.0f, 0.0f, 0.0f);
        gl.glRotatef(angle, 0.0f, 1.0f, 0.0f);
        gl.glRotatef(angle, 0.0f, 0.0f, 1.0f);
        angle++;

        // �]�w���I�H�ί��� Buffer
        setVerticesBuffer();
        setIndexBuffer();

        // �e�X�ߤ���
        // ���w ø�s�ɨϥγ��I�y�Ъ��ƾڮ榡�H�Φ�m
        gl.glVertexPointer(
                3,                          // ���I�ƶq
                GL10.GL_FLOAT,              // ���I����
                0,                          // �_�l��m
                verticesBuffer);            // ���I buffer
        // �z�L���� Buffer ��ø�s�� ( �T���� )
        gl.glDrawElements(
                GL10.GL_TRIANGLES,          // �Ҧ�
                index.length,               // ���Ǽƶq
                GL10.GL_UNSIGNED_SHORT,     // ����
                indexBuffer);               // ���� buffer


        // �������I buffer ���g�J
        gl.glDisableClientState(GL10.GL_VERTEX_ARRAY);
        // ���������� ( FACE )
        gl.glDisable(GL10.GL_CULL_FACE);
    }

    // �]�w���I Buffer
    protected void setVerticesBuffer() {
        // ���`�ٮį�A�ϥ� buffer �s��
        ByteBuffer vbb = ByteBuffer.allocateDirect(vertices.length * 4);
        vbb.order(ByteOrder.nativeOrder());
        verticesBuffer = vbb.asFloatBuffer();
        verticesBuffer.put(vertices);
        verticesBuffer.position(0);
    }

    // �]�w���� Buffer
    protected void setIndexBuffer() {
        // ���`�ٮį�A�ϥ� buffer �s��
        ByteBuffer ibb = ByteBuffer.allocateDirect(index.length * 2);
        ibb.order(ByteOrder.nativeOrder());
        indexBuffer = ibb.asShortBuffer();
        indexBuffer.put(index);
        indexBuffer.position(0);
    }
}
```


![](./picture/GLSurfaceView_finish.png)

#### Contributors
Kevin Chen
#### Troubleshooting

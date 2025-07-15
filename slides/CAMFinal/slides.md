---
title: CAMFinal
background: https://cover.sli.dev
date: 2022-06-19 23:37:33
layout: center
theme: seriph
transition: fade-out
lineNumbers: true
---

# Mesh网格模型切片

### 陈佩佩

---
transition: slide-up
---

## 作业要求

- 实现至少OBJ格式Mesh网格模型的导入和显示（只需要点和面：v和f）
  
  ✔️实现鼠标键盘交互，可以进行平移、旋转、放缩等基础操作

---
transition: slide-up
---

## 作业要求

- 编写程序，实现Mesh网格模型的切片和打印文件导出。
  
  ✔️实现等间距平面和Mesh模型的交线（使用多边形表示）
  
  ✔️通过Clipper实现多边形的内部填充
  
  自定义切片的多边形保存文件，可以进行导入导出，将所有的多边形都进行三维可视化


---
transition: slide-up
---

## 成果展示

<a></a>

<video src="/videos/CAMvideo.mp4" 
    autoplay
    class="rounded-lg shadow-lg" 
    width="750" />

<!-- <iframe id="graph1"
	title="graph1"
	src="/videos/CAMvideo.mp4" 
	height="430px"
	width="100%"
	scrolling="auto" 
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe> -->

---
transition: slide-left
---

# ObjLoader

#### 模型基础显示

![model](/images/model1.png)

---
transition: slide-up
---

## 导入OBJ文件

OBJ文件格式内容

v：点的坐标；f：三角形面片的顶点序号

```cpp
v 0.437500 0.164062 0.765625
v -0.437500 0.164062 0.765625
v 0.500000 0.093750 0.687500
v -0.500000 0.093750 0.687500
v 0.546875 0.054688 0.578125
…………
f 47 1 3
f 4 2 48
f 45 3 5
f 6 4 46
f 3 9 7
f 8 10 4
```

---
transition: slide-up
---

## 导入OBJ文件

格式转换

```cpp {*}{maxHeight:'380px'}
getline(f, line);
vector<string>parameters;
string tailMark = " ";
string ans = "";
line = line.append(tailMark);
for (int i = 0; i < line.length(); i++) {
    char ch = line[i];
    if (ch != ' ') {
        ans+=ch;
    }
    else {
        parameters.push_back(ans);
        ans = "";
    }
}
//cout << parameters.size() << endl;
if (parameters.size() != 4) {
    cout << "the size is not correct" << endl;
}
else {
    if (parameters[0] == "v") {
        vector<GLfloat>Point;
        for (int i = 1; i < 4; i++) {
            GLfloat xyz = atof(parameters[i].c_str());
            Point.push_back(xyz);
        }
        vSets.push_back(Point);
    }
    else if (parameters[0] == "f") {
        vector<GLint>vIndexSets;
        for (int i = 1; i < 4; i++){
            string x = parameters[i];
            string ans = "";
            for (int j = 0; j < x.length(); j++) {
                char ch = x[j];
                if (ch != '/') {
                    ans += ch;
                }
                else {
                    break;
                }
            }
            GLint index = atof(ans.c_str());
            index = index--;
            vIndexSets.push_back(index);
        }
        fSets.push_back(vIndexSets);
    }
}
```

---
transition: slide-up
---

## 导入OBJ文件

绘制模型

```cpp {*}{maxHeight:'380px'}
for (int i = 0; i < fSets.size(); i++) {
    GLfloat VN[3];
    GLfloat SV1[3];
    GLfloat	SV2[3];
    GLfloat SV3[3];
    if ((fSets[i]).size() != 3) {
        cout << "the fSetsets_Size is not correct" << endl;
    }
    else {
        GLint firstVertexIndex = (fSets[i])[0];
        GLint secondVertexIndex = (fSets[i])[1];
        GLint thirdVertexIndex = (fSets[i])[2];
        
        SV1[0] = (vSets[firstVertexIndex])[0];
        SV1[1] = (vSets[firstVertexIndex])[1];
        SV1[2] = (vSets[firstVertexIndex])[2];

        SV2[0] = (vSets[secondVertexIndex])[0];
        SV2[1] = (vSets[secondVertexIndex])[1];
        SV2[2] = (vSets[secondVertexIndex])[2];

        SV3[0] = (vSets[thirdVertexIndex])[0];
        SV3[1] = (vSets[thirdVertexIndex])[1];
        SV3[2] = (vSets[thirdVertexIndex])[2];
        
        GLfloat vec1[3], vec2[3], vec3[3];
        //(x2-x1,y2-y1,z2-z1)
        vec1[0] = SV1[0] - SV2[0];
        vec1[1] = SV1[1] - SV2[1];
        vec1[2] = SV1[2] - SV2[2];

        //(x3-x2,y3-y2,z3-z2)
        vec2[0] = SV1[0] - SV3[0];
        vec2[1] = SV1[1] - SV3[1];
        vec2[2] = SV1[2] - SV3[2];

        //(x3-x1,y3-y1,z3-z1)
        vec3[0] = vec1[1] * vec2[2] - vec1[2] * vec2[1];
        vec3[1] = vec2[0] * vec1[2] - vec2[2] * vec1[0];
        vec3[2] = vec2[1] * vec1[0] - vec2[0] * vec1[1];

        GLfloat D = sqrt(pow(vec3[0], 2) + pow(vec3[1], 2) + pow(vec3[2], 2));

        VN[0] = vec3[0] / D;
        VN[1] = vec3[1] / D;
        VN[2] = vec3[2] / D;

        glNormal3f(VN[0], VN[1], VN[2]);
        
        glVertex3f(SV1[0], SV1[1], SV1[2]);
        glVertex3f(SV2[0], SV2[1], SV2[2]);
        glVertex3f(SV3[0], SV3[1], SV3[2]);
    }
}
```

---
transition: slide-up
---

## 平移

`glTranslatef()` 函数

```cpp
glTranslatef(transX, 0-transY, -5.0f);

switch (temp)
{
	case 'W':
		transY -= 0.05;
		break;
	case 'S':
		transY += 0.05;
		break;
	case 'D':
		transX += 0.05;
		break;
	case 'A':
		transX -= 0.05;
		break;
	default:
		break;
}
```


---
transition: slide-up
---

## 缩放

`glScaled()` 函数

```cpp {*}{maxHeight:'380px'}
glScaled(scaX, scaY, scaZ);

// 滚轮DOWN：4; 滚轮UP：3
if (button == GLUT_LEFT_BUTTON && state == GLUT_DOWN)
{
    oldPosX = x; oldPosY = y;
}
else if (button == 4 && state == GLUT_UP)
{
    scaX -= 0.02;
    scaY -= 0.02;
    scaZ -= 0.02;
    if (scaX < 0.2)
    {
        scaX = 0.2;
        scaY = 0.2;
        scaZ = 0.2;
    }
}
else if (button == 3 && state == GLUT_UP)
{
    scaX += 0.02;
    scaY += 0.02;
    scaZ += 0.02;
    if (scaX > 2)
    {
        scaX = 2;
        scaY = 2;
        scaZ = 2;
    }
}
```

---
transition: slide-up
---

## 旋转

欧拉角

![欧拉角](/images/euler1.png)

---
transition: slide-up
---

## 旋转

`gluLookAt()` 函数

```cpp
gluLookAt(r*cos(c*degree)*cos(c*degree2), r*sin(c*degree2), r*sin(c*degree)*cos(c*degree2), 0.0f, 0.0f, 0.0f, 0.0f, 1.0f, 0.0f);

int temp1 = x - oldPosX;
int temp2 = y - oldPosY;
degree += temp1;
degree2 += temp2;
if (degree2 > 89.0f) degree2 = 89.0f;
if (degree2 < -89.0f) degree2 = -89.0f;

oldPosX = x;
oldPosY = y;
```


---
transition: slide-left
---

# Clipper

#### 模型切片效果

![clip](/images/clip.png)

---
transition: slide-up
---

## 平面模型交线

`MeshPlaneIntersect.h` 获取平面交点

```cpp {*}{maxHeight:'380px'}
struct Plane {
    Vec3D origin = { 0,0,0.5 };
    Vec3D normal = { 0,0,1 };
};

static std::vector<EdgePath> EdgePaths(const std::vector<Face>& faces,
                                       const std::vector<FloatType>& vertexOffsets)
{
    auto crossingFaces = CrossingFaces(faces, vertexOffsets);
    std::vector<EdgePath> edgePaths;
    while (crossingFaces.size() > 0) {
        edgePaths.push_back(GetEdgePath(crossingFaces));
    }
    return edgePaths;
}

typedef std::map<Edge, int> CrossingFaceMap;
static CrossingFaceMap CrossingFaces(const std::vector<Face>& faces,
                                     const std::vector<FloatType>& vertexOffsets) {
    std::vector<std::pair<Edge, int>> crossingFaces;
    for (const auto& face : faces) {
        const bool edge1crosses = vertexOffsets[face[0]] * vertexOffsets[face[1]] < 0;
        const bool edge2crosses = vertexOffsets[face[1]] * vertexOffsets[face[2]] < 0;
        if (edge1crosses || edge2crosses) {
            int oddVertex = edge2crosses - edge1crosses + 1;
            const bool oddIsHigher = vertexOffsets[face[oddVertex]] > 0;
            int v0 = oddVertex + 1 + oddIsHigher;
            if (v0 > 2) {
                v0 -= 3;
            }
            int v2 = oddVertex + 2 - oddIsHigher;
            if (v2 > 2) {
                v2 -= 3;
            }
            crossingFaces.push_back({
                { static_cast<int>(face[v0]), static_cast<int>(face[oddVertex]) },
                static_cast<int>(face[v2]) });
        }
    }
    return CrossingFaceMap(crossingFaces.begin(), crossingFaces.end());
}
```

---
transition: slide-up
---

## 平面模型交线

交点导出到txt

```cpp
Paths sub;
vector<IntPoint> temp;
for (int i = 0; i < result[0].points.size(); i++) {
    int size = result[0].points.size();
    IntPoint temp_point;
    temp_point.X = result[0].points[i][0]*1000+1000;
    temp_point.Y = result[0].points[i][1]*1000+1000;
    temp.push_back(temp_point);
}
sub.push_back(temp);

fstream ff;
ff.open("data/sub.txt", ios::out);
ff << sub << endl;
ff.close();
```

---
transition: slide-up
---

## 多边形内部填充

clipper绘制图像

```cpp {*}{maxHeight:'380px'}
fstream ff;
    ff.open("..\\..\\ObjLoader\\ObjLoader\\data\\sub.txt", ios::in);
    string line;
    if (!ff.is_open()) {
        cout << "Something Went Wrong When Opening Objfiles" << endl;
    }
    vector<string>parameters;
    while (!ff.eof()) {
        getline(ff, line);
        string tailMark = " ";
        string ans = "";
        line = line.append(tailMark);
        for (int i = 0; i < line.length(); i++) {
            char ch = line[i];
            if (ch == '(') {
                ans = "";
            }
            else if (ch == ')') {
                parameters.push_back(ans);
                ans = "";
            }
            else {
                ans += ch;
            }
        }
    }
    ff.close();
    
    vector<IntPoint> vec;
    for (int i = 0; i < parameters.size(); i++)
    {
        IntPoint point;
        vector<string> result = Split(parameters[i], ",");
        point.X = atof(result[0].c_str());
        point.Y = atof(result[1].c_str());
        vec.push_back(point);
    }
    
    sub.clear();
    sub.push_back(vec);
	}

    c.AddPaths(sub, ptSubject, true);
    c.AddPaths(sub, ptClip, true);

    c.Execute(ct, sol, pft, pft);
    SaveToFile("solution.txt", sol);

    if (delta != 0.0)
    {
        ClipperOffset co;
        co.AddPaths(sol, jt, etClosedPolygon);
        co.Execute(sol, delta);
    }

	InvalidateRect(hWnd, NULL, false);
```

---
transition: fade-out
---

# 后续改进

- 实现右键平移模型功能
- 考虑利用OpenCV的`glReadPixels()`函数来完成切片图片保存
- 切片导入导出和多边形三维可视化

---
layout: center
---

# 🎉感谢指导！

#ใบงานที่ 12
##การเขียนโปรแกรมกราฟฟิกส์ด้วย GDI+ (3)
##นางสาวนภารัตน์ ฐิติกรโกวิท 57030180
##กล่าวนำ
ใบงานนี้ มีวัตถุประสงค์ เพื่อให้นักศึกษา ได้รู้จักกับ GDI+ ซึ่งจะช่วยให้นักษาสามารถ
* โหลดภาพชนิดต่างๆ เพื่อมาแสดงบนฟอร์มได้
* จัดการกับภาพโดยวิธีการง่ายๆ เช่น พลิกภาพ หมุนภาพ และเขียนข้อความลงบนภาพได้

###การโหลดภาพเพื่อแสดงบน Form
Project นี้จะโหลดภาพจากไฟล์ (ชนิดใดก็ได้) มาแสดงผลบน Form 
* สร้าง Project ใหม่เป็น Visual C#
* แก้ไข code เพื่อโหลดและแสดงภาพบน Form 
</p align = "center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-12/blob/master/imgs/lab12-1.png">
</p> 

**หมายเหตุ** ในบรรทัดที่ 23 หากนักศึกษาต้องการแสดงไฟล์อื่น ก็ให้ใส่ path พร้อมชื่อ แต่ต้องใส่ \\ แทน \ เนื่องจาก ในภาษา C# นั้น เครื่องหมาย \ จะเป็น escape character เช่นเดียวกับภาษา c และ c++



Code

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Lab12
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Paint(object sender, PaintEventArgs e)
        {
            Bitmap bmp = new Bitmap("d:\\2.JPG");
            this.SetClientSizeCore(bmp.Width + 20, bmp.Height + 20);
            e.Graphics.DrawImage(bmp, 10, 10);
        }
    }
}




```


ผลการทดลอง


![](https://github.com/NAPHARAT/LAB-12/blob/master/imgs/1.JPG)
##การ Zoom ภาพ
การ Zoom ภาพ คือการกำหนดให้ขนาดของพื้นที่แสดงผลต่างไปจากขนาดที่แท้จริงของภาพ (Zoom in, Zoom out) นอกจากนี้เรายังสามารถเลือกส่วนของภาพที่จะแสดงได้อีกด้วย

### การ Zoom out  
คือการกำหนดให้ Rectangle ปลายทาง เล็กกว่าขนาดจริงของภาพ
 </p align = "center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-12/blob/master/imgs/lab12-2.png">
</p> 

Code

```

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Lab12
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Paint(object sender, PaintEventArgs e)
        {
            Bitmap bmp = new Bitmap("d:\\2.JPG");
            Rectangle destrect = new Rectangle(10, 10, bmp.Width / 2, bmp.Height / 2);
            Rectangle srcrect = new Rectangle(0, 0, bmp.Width, bmp.Height);
            this.SetClientSizeCore(destrect.Width + 20, destrect.Height + 20);
            e.Graphics.DrawImage(bmp, destrect, srcrect, GraphicsUnit.Pixel);

            //Bitmap bmp = new Bitmap("d:\\2.JPG");
            //this.SetClientSizeCore(bmp.Width + 20, bmp.Height + 20);
            //e.Graphics.DrawImage(bmp, 10, 10);
        }
    }
}



```


ผลการทดลอง

![](https://github.com/NAPHARAT/LAB-12/blob/master/imgs/2.JPG)
### การ Zoom in  
คือการกำหนดให้ Rectangle ปลายทาง โตกว่า Rectangle ของภาพ ในที่นี้จะเลือกภาพมาแสดง
 
</p align = "center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-12/blob/master/imgs/lab12-3.png">
</p> 




Code

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Lab12
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Paint(object sender, PaintEventArgs e)
        {
            Bitmap bmp = new Bitmap("d:\\2.JPG");
            Rectangle destrect = new Rectangle(10, 10, bmp.Width , bmp.Height );
            Rectangle srcrect = new Rectangle(0, 0, bmp.Width/2, bmp.Height/2);
            this.SetClientSizeCore(destrect.Width + 20, destrect.Height + 20);
            e.Graphics.DrawImage(bmp, destrect, srcrect, GraphicsUnit.Pixel);

        }
    }
}

```

ผลการทดลอง


![](https://github.com/NAPHARAT/LAB-12/blob/master/imgs/3.JPG)

### การพลิกและหมุนภาพ
 </p align = "center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-12/blob/master/imgs/lab12-4.png">
</p> 

Code

```

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Lab12
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Paint(object sender, PaintEventArgs e)
        {
            Bitmap bmp = new Bitmap("d:\\2.JPG");
            this.SetClientSizeCore(bmp.Width, bmp.Height);
            Rectangle topleft = new Rectangle(0, 0, bmp.Width/2, bmp.Height/2);
            Rectangle topright = new Rectangle(bmp.Width / 2,0, bmp.Width  / 2,bmp.Height /2);
            Rectangle bottomleft = new Rectangle(0,bmp.Height /2, bmp.Width / 2, bmp.Height / 2);
            Rectangle bottomright = new Rectangle(bmp.Width / 2, bmp.Height  / 2,bmp.Width /2, bmp.Height / 2);

            bmp.RotateFlip(RotateFlipType.RotateNoneFlipNone);
            e.Graphics.DrawImage(bmp, topleft);

            bmp.RotateFlip(RotateFlipType.RotateNoneFlipX );
            e.Graphics.DrawImage(bmp, topright );

            bmp.RotateFlip(RotateFlipType.Rotate180FlipNone );
            e.Graphics.DrawImage(bmp, bottomleft );

            bmp.RotateFlip(RotateFlipType.Rotate180FlipY );
            e.Graphics.DrawImage(bmp, bottomright );
            
            
           
        }
    }
}

```


ผลการทดลอง


![](https://github.com/NAPHARAT/LAB-12/blob/master/imgs/4.JPG)
## การเขียนข้อความลงในภาพ
 </p align = "center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-12/blob/master/imgs/lab12-5.png">
</p> 

Code

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Lab12
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Paint(object sender, PaintEventArgs e)
        {
            Bitmap bmp = new Bitmap("d:\\2.JPG");
            this.SetClientSizeCore(bmp.Width, bmp.Height);
            Rectangle destrect = new Rectangle(0, 0, bmp.Width, bmp.Height);
            Brush myBrush = new SolidBrush(Color.Coral);
            e.Graphics.DrawImage(bmp, destrect);
            e.Graphics.DrawString("Hello World", new Font("Verdana", 30, FontStyle.Bold), myBrush, 0, 


        }
    }
}

```

ผลการทดลอง

![](https://github.com/NAPHARAT/LAB-12/blob/master/imgs/5.JPG)



##แบบฝึกหัด
ให้วาดตัวการ์ตูน Doraemon โดยใช้คำสั่งต่างๆ ทางด้านกราฟฟิกส์ พร้อมทั้งใส่ชื่อ นามสกุล และรหัสนักศึกษาของตนเองลงไปด้วย (ห้ามใช้วิธีการใส่รูปภาพ)

**[ตัวอย่างงานวาดภาพ Doraemon ของรุ่นพี่](https://github.com/Desktop-Programming-Lab-2559/LAB-12/blob/master/Doraemon.md)**

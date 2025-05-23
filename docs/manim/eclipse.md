---
title: 【Manim】椭圆基础 (视频)
createTime: 2022/01/12 17:56:09
permalink: /article/u0id8v2w/
tags:
    - senior high school
    - manim
    - Python
---

@[bilibili](BV1qZ4y1S7nj)

<!--more-->

这个是我用 `Python` 和 `Manim` 完成的数学笔记视频。做了很长一段时间，在这个过程中也算是积累了一些Python经验

内容为上课记的数学笔记，如有纰漏请在评论区指出~ 感谢观看！

# 源码展示
---
## pages1
```python
from manimlib import *
import numpy as np

class main(Scene):
    def construct(self):
        
        #BGcolor: Default(Black)

        # Prepare for clear the screen 
        self.save_state()

        # Screen Plane (For movements)
        #NumberP = NumberPlane()
        #self.add(NumberP)

        # Title
        title1 = Text("椭圆 · Part I · 定义", font="HarmonyOS Sans SC").scale(2)
        self.play(ShowCreation(title1))
        self.play(title1.animate.scale(0.5).to_corner(UL))

        # axesL&R 
        # Origin:L4U1 R4U1
        # withOUT lables 
        # Color:Default
        axesL = Axes(
            x_range=(-3,3,0.5), 
            y_range=(-2,2,0.5), 
            height=4,
            width=6 )
        axesR = axesL.copy()
        axesL.shift(UP+LEFT*4)
        axesR.shift(UP+RIGHT*4)
        self.play(
            ShowCreation(axesL),
            Write(axesL.get_axis_labels()))
        self.wait(0.5)
        
        # Focus Point:
        f = np.sqrt(7)/2
        dF1 = Dot(axesL.c2p(-f,0))
        dF2 = Dot(axesL.c2p(f,0))
        tF1 = Tex(r"F1").scale(0.5).next_to(dF1, direction=DOWN*1/2)
        tF2 = Tex(r"F2").scale(0.5).next_to(dF2, direction=DOWN*1/2)
        gF = VGroup(dF1, tF1, dF2, tF2)
        self.play(ShowCreation(gF))
        self.wait(0.5)

        # P点
        ellipseL = Ellipse(width=4,height=3).set_color(BLUE).move_to(axesL)
        ellipseR = Ellipse(width=3, height=4).set_color(GREEN).shift(UP+RIGHT*4)
        dP = Dot(color=ORANGE).move_to(ellipseL.pfp(0.3))
        tP = Tex(r"P").scale(0.5).next_to(dP, direction=DOWN*1/2)
        P = VGroup(dP, tP)
        self.play(ShowCreation(P))

        #PF
        PF1 = Line(start=dP, end=dF1)
        PF2 = Line(start=dP, end=dF2)
        PF = VGroup(PF1, PF2)
        PF.set_color(ORANGE)
        self.play(ShowCreation(PF))
        self.wait(0.5)

        # Definition Tex 
        tDefine = Tex(r"\left|{\rm PF}_1\right|+\left|{\rm PF}_2\right|=2a", color=BLUE).to_edge(UP).scale(0.75).shift(RIGHT*3)
        self.play(Write(tDefine))
        self.wait(1)
        
        # Ellipse
        self.play(ShowCreation(ellipseL))
        self.wait(0.5)

        #公式推导
        func_derivation = VGroup(
            Tex(r"\sqrt{{(x+c)}^2+y^2}+\sqrt{{(x-c)}^2+y^2}=2a"),                                    #0 l02
            Tex(r"\sqrt{{(x+c)}^2+y^2}=2a-\sqrt{{(x-c)}^2+y^2}"),                                    #1 l03
            Tex(r"\left(\sqrt{{(x+c)}^2+y^2}\ \right)^2=\left(2a-\sqrt{{(x-c)}^2+y^2}\right)^2"),    #2 l04
            Tex(r"a\sqrt{\left(x-c\right)^2+y^2}=a^2-cx"),                                           #3 l04(Transform)
            Tex(r"\left(a\sqrt{\left(x-c\right)^2+y^2}\right)^2=\left(a^2-cx\right)^2"),             #4 l05
            Tex(r"\left(a^2-c^2\right)x^2+a^2y^2=a^2(a^2-c^2)"),                                     #5 l05(Transform)
            Text(r"令", font="HarmonyOS Sans SC"),                                                   #6
            Tex(r"b=a^2-c^2")                                                                        #7
            #Tex(r"\frac{x^2}{a^2}+\frac{y^2}{b^2}=1")                                               #l07
        )
        func_derivation.match_x(tDefine)
        func_derivation.to_edge(UP)
        func_derivation.set_color(BLUE)
        func_derivation.scale(0.75)
        func_derivation[0].shift(DOWN*1)
        func_derivation[1].shift(DOWN*2)
        func_derivation[2].shift(DOWN*3)
        func_derivation[3].shift(DOWN*3)
        func_derivation[4].shift(DOWN*4)
        func_derivation[5].shift(DOWN*4)
        func_derivation[6].shift(DOWN*5)
        func_derivation[7].next_to(func_derivation[6])
        func_origin = Tex(r"\frac{x^2}{a^2}+\frac{y^2}{b^2}=1", isolate=["\frac{x^2}{a^2}+\frac{y^2}{b^2}=1"],color=WHITE).scale(0.75).match_x(tDefine).to_edge(UP).shift(DOWN*6)
        
        self.play(Write(func_derivation[0]))
        self.play(Write(func_derivation[1]))
        self.play(Write(func_derivation[2]))
        self.play(TransformMatchingTex(func_derivation[2], func_derivation[3], transform_mismatches=True))
        self.play(Write(func_derivation[4]))
        self.play(TransformMatchingTex(func_derivation[4], func_derivation[5], transform_mismatches=True))
        self.play(Write(func_derivation[6]))
        self.play(Write(func_derivation[7]))
        self.play(TransformFromCopy(func_derivation[4], func_origin))

        self.play(ShowCreationThenDestructionAround(func_origin))
        self.play(FadeOutToPoint(func_derivation, axesL.get_center()))

        # Standard Function
        funcL = Tex(r"\frac{x^2}{a^2}+\frac{y^2}{b^2}=1(a>b>0)", isolate=["\frac{x^2}{a^2}+\frac{y^2}{b^2}=1"],color=BLUE).scale(0.75)
        funcL.move_to(func_origin)
        funcR = Tex(r"\frac{y^2}{a^2}+\frac{x^2}{b^2}=1(a>b>0)",color=GREEN).scale(0.75)
        funcR.move_to(axesR).shift(DOWN*2.5)

        self.play(TransformMatchingTex(func_origin, funcL))
        self.play(funcL.animate.move_to(axesL).shift(DOWN*2.5).set_color(BLUE))
        self.play(tDefine.animate.shift(LEFT*3).set_color(WHITE))
        self.play(ShowCreationThenDestructionAround(tDefine))
        self.wait(0.5)

        self.play(
            ShowCreation(axesR),
            Write(axesR.get_axis_labels()))
        gR = VGroup(ellipseR, funcR)
        self.play(ShowCreation(gR))
        self.wait(1.5)
        self.restore()
        self.wait(0.5)
```

---
## pages2
```python
from math import gamma
from re import A
from manimlib import *
import numpy as np

class main(Scene):
    def construct(self):
        #self.save_state()
        
        #BGcolor: Default(Black)

        # Screen Plane (For movements)
        #NumberP = NumberPlane()
        #self.add(NumberP)

        # Title
        title2 = Text("椭圆 · Part I · 基本性质", font="HarmonyOS Sans SC").scale(2)
        self.play(ShowCreation(title2))
        self.play(title2.animate.scale(0.5).to_corner(UL))
        
        # AxesL
        axesL = Axes(
            x_range=(-3,3,0.5), 
            y_range=(-2,2,0.5), 
            height=4,
            width=6 ).shift(UP*0.5+LEFT*4)
        self.play(
            ShowCreation(axesL),
            Write(axesL.get_axis_labels()))
        #self.wait(0.5)

        # Ellipse
        a = 2
        b = 1.5
        ellipseL = Ellipse(width=4,height=3).set_color(BLUE).move_to(axesL)
        self.play(ShowCreation(ellipseL))

        # Focus Point:
        f = np.sqrt(7)/2
        dF1 = Dot(axesL.c2p(-f,0)).set_color(ORANGE)
        dF2 = Dot(axesL.c2p(f,0)).set_color(ORANGE)
        tF1 = Tex(r"F1").set_color(ORANGE).scale(0.5).next_to(dF1, direction=DOWN*1/2)
        tF2 = Tex(r"F2").set_color(ORANGE).scale(0.5).next_to(dF2, direction=DOWN*1/2)
        gF = VGroup(dF1, tF1, dF2, tF2)
        self.play(ShowCreation(gF))
        
        # Standard Function
        funcL = Tex(r"\frac{x^2}{a^2}+\frac{y^2}{b^2}=1(a>b>0)", isolate=["\frac{x^2}{a^2}+\frac{y^2}{b^2}=1"],color=BLUE).scale(0.75).move_to(axesL).shift(DOWN*2.5)
        funcL.move_to(axesL).shift(DOWN*3)
        self.play(Write(funcL))
        self.wait(0.5)

        # Centre Line
        line = Line(start=UP*4, end=DOWN*4)
        self.play(ShowCreation(line))

        # Sub title:
        stitle = Text("基本性质", font="HarmonyOS Sans SC").to_edge(UP).shift(RIGHT*3.5)
        self.play(TransformFromCopy(title2, stitle))
        self.wait(1)

        self.save_state()

        # 焦点焦距
        self.play(*[ApplyWave(mob) for mob in gF])
        焦点 = Text("F1,F2 (±c,0): 焦点", font="HarmonyOS Sans SC").set_color(ORANGE).scale(0.75).move_to(stitle).shift(DOWN+LEFT*1.5)
        self.play(Write(焦点))
        焦距线 = Line(start=dF1, end=dF2).set_color(ORANGE)
        焦距1 = Tex(r"\left|F_1F_2\right|").scale(0.75).next_to(焦点).set_color(ORANGE)
        焦距2 = Text(": 焦距", font="HarmonyOS Sans SC").scale(0.75).next_to(焦距1).set_color(ORANGE)
        self.play(ShowCreationThenDestruction(焦距线), run_time=1.5, rate_func=double_smooth)
        self.play(Write(焦距1), Write(焦距2))
        self.wait(1)

        # 左右顶点
        dA1 = Dot(axesL.c2p(-2,0)).set_color(GREEN)
        dA2 = Dot(axesL.c2p(2,0)).set_color(GREEN)
        tA1 = Tex(r"A_1").set_color(GREEN).scale(0.5).next_to(dA1, direction=DOWN*1/2)
        tA2 = Tex(r"A_2").set_color(GREEN).scale(0.5).next_to(dA2, direction=DOWN*1/2)
        gA = VGroup(dA1, tA1, dA2, tA2)
        self.play(ShowCreation(gA))
        左右顶点 = Text("A1,A2 (±a,0): 左右顶点", font="HarmonyOS Sans SC").set_color(GREEN).scale(0.75).move_to(焦点).shift(DOWN)
        self.play(Write(左右顶点))
        长轴 = Line(start=dA1, end=dA2).set_color(GREEN)
        长轴1 = Tex(r"\left|A_1A_2\right|").scale(0.75).next_to(左右顶点).set_color(GREEN)
        长轴2 = Text(": 长轴", font="HarmonyOS Sans SC").scale(0.75).next_to(长轴1).set_color(GREEN)
        self.play(ShowCreationThenDestruction(长轴), run_time=1.5, rate_func=double_smooth)
        self.play(Write(长轴1), Write(长轴2))
        self.wait(1)

        # 上下顶点
        dB1 = Dot(axesL.c2p(0,-1.5)).set_color(GOLD)
        dB2 = Dot(axesL.c2p(0,1.5)).set_color(GOLD)
        tB1 = Tex(r"B_1").set_color(GOLD).scale(0.5).next_to(dB1, direction=DOWN*1/2)
        tB2 = Tex(r"B_2").set_color(GOLD).scale(0.5).next_to(dB2, direction=DOWN*1/2)
        gB = VGroup(dB1, tB1, dB2, tB2)
        self.play(ShowCreation(gB))
        上下顶点 = Text("B1,B2 (±b,0): 上下顶点", font="HarmonyOS Sans SC").set_color(GOLD).scale(0.75).move_to(左右顶点).shift(DOWN)
        self.play(Write(上下顶点))
        短轴 = Line(start=dB1, end=dB2).set_color(GOLD)
        短轴1 = Tex(r"\left|B_1B_2\right|").scale(0.75).next_to(上下顶点).set_color(GOLD)
        短轴2 = Text(": 短轴", font="HarmonyOS Sans SC").scale(0.75).next_to(短轴1).set_color(GOLD)
        self.play(ShowCreationThenDestruction(短轴), run_time=1.5, rate_func=double_smooth)
        self.play(Write(短轴1), Write(短轴2))
        self.wait(2)

        self.restore()

        # 离心率部分
        # e_t:标题
        # e_d：定义公式
        e_t = Text("离心率", font="HarmonyOS Sans SC").scale(0.85).move_to(line, aligned_edge=LEFT).to_edge(UP).shift(DOWN*1.5+RIGHT*0.25)
        self.play(Write(e_t))
        e_d = Tex(r"e=\frac{c}{a}", isolate=["e="]).scale(0.75).next_to(e_t)
        self.play(Write(e_d))
        e_d2 = Tex(r"=\frac{\left|F_1F_2\right|}{\left|PF_1\right|+\left|PF_2\right|}").scale(0.75).next_to(e_d)#.move_to(stitle).shift(DOWN*2)
        self.play(TransformFromCopy(e_d, e_d2))

        # 焦点三角形
        M1 = Dot(color=YELLOW_D).move_to(ellipseL.pfp(0.3))
        M2 = Dot(color=YELLOW_D).move_to(ellipseL.pfp(0.58))
        CMF = Polygon(M1.get_center(), M2.get_center(), dF2.get_center()).set_color(YELLOW_D)
        CMF_t = Text("焦点三角形", font="HarmonyOS Sans SC").scale(0.85).move_to(line, aligned_edge=LEFT).shift(RIGHT*0.25).match_y(e_d).shift(DOWN)
        CMF_d = Tex(r"C_{\triangle ABF_2}=4a").scale(0.75).next_to(CMF_t)
        self.play(Write(CMF_t))
        self.play(ShowCreation(M1), ShowCreation(M2))
        self.play(ShowCreation(CMF))
        self.play(Write(CMF_d))
        self.wait(2)
        CMF_a = VGroup(M1, M2, CMF)
        self.play(*[FadeOut(mob) for mob in CMF_a])

        # 通经
        h = b*b/a
        dH1 = Dot(axesL.c2p(-f,h), color=YELLOW_D)
        dH2 = Dot(axesL.c2p(-f,-h), color=YELLOW_D)
        lH = Line(dH1, dH2).set_color(YELLOW_D)
        gH = VGroup(dH1, dH2, lH)
        h_t = Text("通径", font="HarmonyOS Sans SC").scale(0.85).move_to(line, aligned_edge=LEFT).shift(RIGHT*0.25).match_y(CMF_t).shift(DOWN)
        self.play(Write(h_t))
        self.play(ShowCreation(gH))
        h_d = Tex(r"=\frac{2b^2}{a}").scale(0.75).next_to(h_t)
        self.play(Write(h_d))
        self.wait(2)
        self.play(*[FadeOut(mob) for mob in gH])

        # 椭圆上一点到焦点性质
        P = Dot(color=YELLOW_D).move_to(ellipseL.pfp(0.15))
        P_l = Tex(r"P").scale(0.7).set_color(YELLOW_D).next_to(P)
        PF1 = Line(P, dF1).set_color(YELLOW_D)
        PF2 = Line(P, dF2).set_color(YELLOW_D)
        gP = VGroup(P, PF1, PF2, P_l)
        p_t = Text("椭圆上一点P", font="HarmonyOS Sans SC").scale(0.85).move_to(line, aligned_edge=LEFT).shift(RIGHT*0.25).match_y(h_t).shift(DOWN)
        self.play(ShowCreation(gP))
        self.play(Write(p_t))
        p_1 = Tex(r"\left|PF\right|\in\ \left[a-c,a+c\right]").scale(0.75).move_to(line, aligned_edge=LEFT).shift(RIGHT).match_y(p_t).shift(DOWN)
        self.play(Write(p_1))
        p_2 = Tex(r"\left|PF_1\right|\bullet\left|PF_2\right|=\left[b^2,a^2\right]").scale(0.75).move_to(line, aligned_edge=LEFT).shift(RIGHT).match_y(p_1).shift(DOWN)
        self.play(Write(p_2))
        self.wait(2)

        self.restore()
        
        # 面积
        self.play(ShowCreation(gP))
        a_1 = PF1.get_angle()
        a1=a_1
        a_2 = PF2.get_angle()
        a2 = a_2-a_1
        theta = Arc(start_angle=a1, angle=a2, arc_center=P.get_center(), radius=0.5)
        t_l = Tex(r"\theta").scale(0.7).set_color(GREEN).next_to(theta, DOWN)
        gt = VGroup(theta, t_l)
        self.play(ShowCreation(gt))
        S_d = Tex(r'S_{\triangle F_1PF_2}=b^2\bullet tan\frac{\theta}{2}', t2c={'\theta':GREEN}).scale(0.85).move_to(line, aligned_edge=LEFT).to_edge(UP).shift(DOWN*1.5+RIGHT*0.25)
        self.play(Write(S_d))
        func_derivation = VGroup(
            Tex(r"S_{\triangle F_1PF_2}=\frac{1}{2}\bullet\left|PF_1\right|\bullet\left|PF_2\right|\bullet\sin{\theta}", isolate=["\left|PF_1\right|\bullet\left|PF_2\right|"]).scale(0.6).match_x(stitle).to_edge(UP).shift(DOWN*2.5), #0
            Tex(r"\left|F_1F_2\right|^2=\left|PF_1\right|^2+\left|PF_2\right|^2-2\left|PF_1\right|\bullet\left|PF_2\right|\bullet\cos{\theta}", isolate=["\left|F_1F_2\right|^2=", "\left|PF_1\right|\bullet\left|PF_2\right|", "\bullet\cos{\theta}"]).scale(0.6).match_x(stitle).to_edge(UP).shift(DOWN*3.5),#1
            Tex(r"{\left|F_1F_2\right|^2=\left(\left|PF_1\right|+\left|PF_2\right|\right)}^2-2\left|PF_1\right|\bullet\left|PF_2\right|\bullet\left(1+\cos{\theta}\right)", isolate=["\left|F_1F_2\right|^2=", "\left|PF_1\right|\bullet\left|PF_2\right|", "\left(1+\cos{\theta}\right)"]).scale(0.5).match_x(stitle).to_edge(UP).shift(DOWN*4.5),#2
            Tex(r"{4c}^2={4a}^2-2\left|PF_1\right|\bullet\left|PF_2\right|\bullet\left(1+\cos{\theta}\right)", isolate=["\left|PF_1\right|\bullet\left|PF_2\right|", "\left(1+\cos{\theta}\right)"]).scale(0.6).match_x(stitle).to_edge(UP).shift(DOWN*5.5),
            Tex(r"\left|PF_1\right|\bullet\left|PF_2\right|=\frac{2b^2}{\left(1+\cos{\theta}\right)}").scale(0.6).match_x(stitle).to_edge(UP).shift(DOWN*6.5)
        )
        
        self.play(Write(func_derivation[0]))
        self.play(TransformFromCopy(func_derivation[0], func_derivation[1]))
        self.play(TransformFromCopy(func_derivation[1], func_derivation[2]))
        self.play(TransformFromCopy(func_derivation[2], func_derivation[3]))
        self.play(TransformFromCopy(func_derivation[3], func_derivation[4]))
        self.play(ShowCreationThenDestructionAround(func_derivation[4]))
        self.play(Indicate(S_d))
        self.wait(2)

        self.restore()
        self.add(P)
        PA = VGroup(
            Line(P, dA1),
            Line(P,dA2)
        )
        PA.set_color(YELLOW_D)
        PA_d = Tex(r"k_{PA_1}\bullet k_{PA_2}=-\frac{b^2}{a^2}").scale(0.8).move_to(line, aligned_edge=LEFT).to_edge(UP).shift(DOWN*1.5+RIGHT*0.25)
        self.play(ShowCreation(gA))
        self.play(ShowCreation(PA))
        
        self.play(Write(PA_d))
        self.wait(2)

```
from manim import *

class AnimatedEquations(Scene):
    def construct(self):
        # ===== المشهد 1: عنوان =====
        title = Text("معادلات رياضية متحركة", font_size=48, color=YELLOW)
        subtitle = Text("Mathematical Animations", font_size=28, color=BLUE_B)
        subtitle.next_to(title, DOWN, buff=0.3)

        self.play(Write(title), run_time=1.5)
        self.play(FadeIn(subtitle, shift=UP*0.3))
        self.wait(1)
        self.play(FadeOut(title), FadeOut(subtitle))

        # ===== المشهد 2: معادلة تربيعية =====
        eq1 = MathTex(r"ax^2 + bx + c = 0", font_size=60, color=WHITE)
        label1 = Text("المعادلة التربيعية", font_size=28, color=GOLD)
        label1.next_to(eq1, UP, buff=0.5)

        self.play(Write(label1))
        self.play(Write(eq1), run_time=2)
        self.wait(1)

        # تحويل إلى صيغة الحل
        eq2 = MathTex(
            r"x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}",
            font_size=55, color=YELLOW
        )
        arrow = Arrow(eq1.get_bottom(), eq2.get_top(), buff=0.2, color=GREEN)

        self.play(
            eq1.animate.shift(UP * 1.5),
            label1.animate.shift(UP * 1.5)
        )
        self.play(GrowArrow(arrow))
        self.play(Write(eq2), run_time=2.5)
        self.wait(1.5)
        self.play(FadeOut(eq1), FadeOut(eq2), FadeOut(arrow), FadeOut(label1))

        # ===== المشهد 3: نظرية فيثاغورس =====
        pyth_label = Text("نظرية فيثاغورس", font_size=32, color=GREEN_B)
        pyth_label.to_edge(UP)
        self.play(Write(pyth_label))

        # المثلث
        triangle = Polygon(
            ORIGIN, RIGHT * 3, RIGHT * 3 + UP * 2,
            color=WHITE
        )
        triangle.move_to(LEFT * 2)

        a_label = MathTex("a", color=RED, font_size=40)
        b_label = MathTex("b", color=BLUE, font_size=40)
        c_label = MathTex("c", color=YELLOW, font_size=40)

        a_label.next_to(triangle, DOWN, buff=0.15)
        b_label.next_to(triangle, RIGHT, buff=0.15)
        c_label.move_to(triangle.get_center() + LEFT * 0.5 + UP * 0.3)

        self.play(DrawBorderThenFill(triangle))
        self.play(Write(a_label), Write(b_label), Write(c_label))

        # المعادلة
        pyth_eq = MathTex(r"a^2 + b^2 = c^2", font_size=56, color=WHITE)
        pyth_eq.move_to(RIGHT * 2.5)

        self.play(Write(pyth_eq), run_time=2)

        # تمييز كل حد بلون
        pyth_colored = MathTex(
            r"a^2", r" + ", r"b^2", r" = ", r"c^2",
            font_size=56
        )
        pyth_colored[0].set_color(RED)
        pyth_colored[2].set_color(BLUE)
        pyth_colored[4].set_color(YELLOW)
        pyth_colored.move_to(RIGHT * 2.5)

        self.play(TransformMatchingTex(pyth_eq, pyth_colored))
        self.wait(1.5)
        self.play(FadeOut(triangle), FadeOut(a_label), FadeOut(b_label),
                  FadeOut(c_label), FadeOut(pyth_colored), FadeOut(pyth_label))

        # ===== المشهد 4: قانون أويلر =====
        euler_label = Text("هوية أويلر الأجمل في الرياضيات", font_size=30, color=BLUE_B)
        euler_label.to_edge(UP)
        self.play(Write(euler_label))

        euler = MathTex(
            r"e^{i\pi} + 1 = 0",
            font_size=80, color=WHITE
        )
        self.play(Write(euler), run_time=3)

        # إضاء ونبض
        self.play(euler.animate.set_color(YELLOW).scale(1.2), run_time=0.5)
        self.play(euler.animate.set_color(WHITE).scale(1/1.2), run_time=0.5)

        # شرح الأجزاء
        parts = VGroup(
            MathTex(r"e", color=RED, font_size=36),
            MathTex(r"i", color=GREEN, font_size=36),
            MathTex(r"\pi", color=BLUE, font_size=36),
            MathTex(r"1", color=ORANGE, font_size=36),
            MathTex(r"0", color=PURPLE, font_size=36),
        )
        descs = VGroup(
            Text("عدد أويلر", font_size=22, color=RED),
            Text("الوحدة التخيلية", font_size=22, color=GREEN),
            Text("النسبة التقريبية", font_size=22, color=BLUE),
            Text("الواحد", font_size=22, color=ORANGE),
            Text("الصفر", font_size=22, color=PURPLE),
        )

        for i, (p, d) in enumerate(zip(parts, descs)):
            p.move_to(LEFT * 4 + RIGHT * i * 2 + DOWN * 2)
            d.next_to(p, DOWN, buff=0.15)

        self.play(euler.animate.shift(UP * 1))
        self.play(LaggedStart(*[FadeIn(p) for p in parts], lag_ratio=0.3))
        self.play(LaggedStart(*[FadeIn(d) for d in descs], lag_ratio=0.3))
        self.wait(2)

        self.play(FadeOut(euler), FadeOut(parts), FadeOut(descs), FadeOut(euler_label))

        # ===== المشهد 5: خاتمة =====
        end_text = Text("استمر في التعلم! 🚀", font_size=52, color=GOLD)
        self.play(Write(end_text), run_time=1.5)
        self.play(end_text.animate.scale(1.1).set_color(YELLOW))
        self.wait(1)
        self.play(FadeOut(end_text))Installation
============

Depending on your use case, different installation options are recommended:
if you just want to play around with Manim for a bit, interactive in-browser
notebooks are a really simple way of exploring the library as they
require no local installation. Head over to
https://try.manim.community to give our interactive tutorial a try.

Otherwise, if you intend to use Manim to work on an animation project,
we recommend installing the library locally (preferably to some isolated
virtual Python environment, or a conda-like environment, or via Docker).

.. warning::

   Note that there are several different versions of Manim. The
   instructions on this website are **only** for the *community edition*.
   Find out more about the :ref:`differences between Manim
   versions <different-versions>` if you are unsure which
   version you should install.

#. :ref:`(Recommended) Installing Manim via Python's package manager pip
   <local-installation>`
#. :ref:`Installing Manim to a conda environment <conda-installation>`
#. :ref:`Using Manim via Docker <docker-installation>`
#. :ref:`Interactive Jupyter notebooks via Binder / Google Colab
   <interactive-online>`


.. _local-installation:

Installing Manim locally via pip
********************************

The recommended way of installing Manim is by using Python's package manager
pip. If you already have a Python environment set up, you can simply run
``pip install manim`` to install the library.

Our :doc:`local installation guide <installation/uv>` provides more detailed
instructions, including best practices for setting up a suitable local environment.

.. toctree::
   :hidden:

   installation/uv

.. _conda-installation:

Installing Manim via Conda and related environment managers
***********************************************************

Conda is a package manager for Python that allows creating environments
where all your dependencies are stored. Like this, you don't clutter up your PC with
unwanted libraries and you can just delete the environment when you don't need it anymore.
It is a good way to install manim since all dependencies like ``pycairo``, etc. come with it.
Also, the installation steps are the same, no matter if you are
on Windows, Linux, Intel Macs or on Apple Silicon.

.. NOTE::

   There are various popular alternatives to Conda like
   `mamba <https://mamba.readthedocs.io/en/latest/>`__ /
   `micromamba <https://mamba.readthedocs.io/en/latest/user_guide/micromamba.html>`__,
   or `pixi <https://pixi.sh>`__.
   They all can be used to setup a suitable, isolated environment
   for your Manim projects.

The following pages show how to install Manim in a conda environment:

.. toctree::
   :maxdepth: 2

   installation/conda


.. _docker-installation:

Using Manim via Docker
**********************

`Docker <https://www.docker.com>`__ is a virtualization tool that
allows the distribution of encapsulated software environments (containers).

The following pages contain more information about the docker image
maintained by the community, ``manimcommunity/manim``:

.. toctree::

   installation/docker


.. _interactive-online:

Interactive Jupyter notebooks for your browser
**********************************************

Manim ships with a built-in ``%%manim`` IPython magic command
designed for the use within `Jupyter notebooks <https://jupyter.org>`__.
Our interactive tutorial over at https://try.manim.community illustrates
how Manim can be used from within a Jupyter notebook.

The following pages explain how you can setup interactive environments
like that yourself:

.. toctree::

   installation/jupyter

.. _editor-addons:

Editors
********

If you're using Visual Studio Code you can install an extension called
*Manim Sideview* which provides automated rendering and an integrated preview
of the animation inside the editor. The extension can be installed through the
`marketplace of VS Code <https://marketplace.visualstudio.com/items?itemName=Rickaym.manim-sideview>`__.

.. caution::

   This extension is not officially maintained by the Manim Community.
   If you run into issues, please report them to the extension's author.


Installation for developers
***************************

In order to change code in the library, it is recommended to
install Manim in a different way. Please follow the instructions
in our :doc:`contribution guide <contributing>` if you are
interested in that.

<html>
<head>
<script type="text/javascript">
    var x = 0;
    var y = 0;
    var phase = "right";
    function changepic() {
        var dirs = ["up", "down", "right", "left"];
        for (var i = 0; i < 4; i++) {
            var img = document.getElementById(dirs[i]);
            img.style.position = "absolute";
            img.style.display = phase == dirs[i] ? "inline" : "none";
            img.style.left = x;
            img.style.top = y;
        }

        if (phase == "right") {
            x += 1;
            if (x == 640) {
                phase = "down";
            }
        }
        if (phase == "down") {
            y += 1;
            if (y == 480) {
                phase = "left";
            }
        }
        if (phase == "left") {
            x -= 1;
            if (x == 0) {
                phase = "up";
            }
        }
        if (phase == "up") {
            y -= 1;
            if (y == 0) {
                phase = "right";
            }
        }
    }
    setInterval(changepic, 20);
</script>
</head>
<body style="width:700px">
<h1>algif5</h1>
<div style="float:right">
<pre>
struct ALGIF_ANIMATION {
    int width, height;
    int frames_count;
    int background_index;
    /* -1 = no, 0 = forever,
     * 1..65535 = that many times
     */
    int loop;
    ALGIF_PALETTE palette;
    ALGIF_FRAME *frames;
    int duration;
};
struct ALGIF_FRAME {
    ALGIF_BITMAP *bitmap_8_bit;
    ALGIF_PALETTE palette;
    int xoff, yoff;
    /* in 1/100th seconds */
    int duration;
    /* 0 = don't care, 1 = keep,
     * 2 = background, 3 = previous
     */        
    int disposal_method;
    int transparent_index;
};
struct ALGIF_BITMAP {
    int w, h, d;
    uint8_t *data;
};
struct ALGIF_PALETTE {
    int colors_count;
    ALGIF_RGB colors[256];
};
struct ALGIF_RGB {
    uint8_t r, g, b;
};
</pre>
</div>
<h2>About</h2>
<b>algif5</b> is a gif loading library for Allegro 5.
<h2>Download</h2>
<a href="algif5.zip">algif5.zip</a>
<h2>Documentation</h2>
There is basically only three functions:
<pre>ALGIF_ANIMATION *gif = algif_load_animation(char const *filename);
ALGIF_ANIMATION *gif = algif_load_animation_f(ALLEGRO_FILE *file);
</pre>
<p>Load a gif.</p>
<pre>al_draw_bitmap(algif_get_bitmap(gif, al_get_time()), x, y, 0);</pre>
<p>Draw the current frame.</p>
<pre>algif_destroy_animation(gif);</pre>
<p>Destroy the gif again.</p>
<p>Like the version without _f but load from an ALLEGRO_FILE instead.</p>
<h2>Installation</h2>
Unfortunately I'm bad with build systems and makefiles and so on, so instead
just do this:
<ul>
    <li>Place algif.h somewhere where your compiler will find it.</li>
    <li>When compiling your code, make sure algif.c, bitmap.c, gif.c and lzw.c
    are compiled along.</li>
</ul>
I also included a makefile in the .zip to create the example program but it
probably only works in Linux. Allegro 5 (including the primitives addon) is
required.
<h2>Examples</h2>
<p>The download comes with an example program.</p>
<img id="up" src="examples/skeleton_up.gif" />
<img id="down" src="examples/skeleton_down.gif" />
<img id="left" src="examples/skeleton_left.gif" />
<img id="right" src="examples/skeleton_right.gif" />
</body>
</html>

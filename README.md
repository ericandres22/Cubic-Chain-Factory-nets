# Polycube chains — three unfoldings

Companion application to the paper **Introducing Factory-Nets**
by Eric Andres and Gaëlle Largeteau-Skapin
(XLIM, UMR CNRS 7252, ASALI team, University of Poitiers).

Draw a chain of face-connected cubes and the application unfolds it, without overlap, in the
three ways studied in the paper. Each net is assembled from a small fixed set of
**factory-nets**: planar cut-outs (outline and fold lines) taken up to rotation and
translation, so that identical pieces are counted once. The application shows which cut-out
each cube uses, where it is hinged to its neighbours, and folds the net back onto the chain.

## Running it

The application is the single file `cube_three_ways.html`. Open it in any recent browser; it
needs no installation, no server and no network connection.

To publish it with GitHub Pages, enable Pages for the repository and open
`https://<user>.github.io/<repository>/cube_three_ways.html` (or rename the file
`index.html`).

## Using it

1. **Draw the chain.** The chain starts with one cube at the origin. Click a highlighted face
   of the last cube to add a cube behind it. **Undo**, **Reset** and **Random** (a random
   chain of 3 to 6 cubes) are in the header. The centres of the cubes are listed at the top
   left of the 3D view, and an *x, y, z* marker in the lower right corner turns with the view.
   Drag to orbit, scroll to zoom.
2. **Choose a construction** in the second bar (see below).
3. **Build** (①) draws the net in the lower panel. After the first build, every change to the
   chain or to the construction rebuilds it.
4. In the face-perfect construction, **Remove walls** (②) deletes the two copies of every wall
   and slides the pieces together.
5. The **unfold** slider opens the chain into its net, and folds it back.
6. **face #** shows the face numbers on the net; **download SVG** saves the net;
   **−**, **fit** and **+** zoom the net.

In the net, each piece is labelled with its cube and its factory-net or version, for instance
`C3 · v4`. Fold lines are thin, cuts are thick, the port through which a piece is entered is
blue and the port through which it is left is red. Faces are numbered 1 to 6 with outward
normals +x, +y, +z, −z, −y, −x, so that opposite faces add up to 7; the header lists the walls
of the chain as `F1 F2 …`, the face of each cube through which the next one is reached.

## The three constructions

| mode | surface unfolded | faces | factory-nets | versions |
|---|---|---|---|---|
| solid · edge-perfect | every face of every cube, each wall twice | 6n | 1 | 5 |
| classical, via removal · face-perfect | boundary surface, after ② | 4n+2 | 6 | 8 |
| classical, direct · edge-perfect | boundary surface | 4n+2 | 4 | 9 |

Here *n* is the number of cubes; versions are counted for the interior cubes, plus the end
piece of the direct construction, as in the paper.

* **Solid, edge-perfect.** One factory-net, the 3–3 hexomino (two rows of three squares
  offset by two), in five versions `v2`, `v4`, `v6`, `v8`, `v10`, one per wall: the table of
  Fig. 1 of the paper. Every piece lies in its own vertical slab, between its entry and exit
  ports, so the net cannot overlap itself. No look-ahead is needed.
* **Classical, via removal, face-perfect.** Six factory-nets `Q1`–`Q6` (Fig. 2), whose two rail
  faces stand alone in their columns. Pressing ② deletes the wall copies (shown in red) and
  slides each piece by 2; the result is a net of the boundary surface.
* **Classical, direct.** The pieces left once the walls of `Q1`–`Q6` are deleted: the
  tetrominoes `I`, `T`, `Z` for the interior cubes and the pentomino `Y` for both ends
  (Fig. 3). They are stamped directly, with the same choice at every step as the
  face-perfect construction, so the net obtained with ② in face-perfect mode is **exactly** the
  net of the direct mode (Proposition 29 of the paper).

The first cube has no entry port, so its rail is free; the application picks the first one
that works. The net of a chain is therefore not unique in general: another rail, or another
version where a wall is served by several, gives another valid net.

## Checking the constructions without a browser

The `tools` folder runs the application's own construction code under Node.js (version 16 or
later):

```
node tools/check.js            # 300 random chains of 3 to 12 cubes, in all three modes
node tools/check.js 1000 42    # 1000 chains, random seed 42
node tools/run_app.js cube_three_ways.html direct '[1,2,1,4]'   # one strip, as JSON
```

`check.js` verifies, for every chain and every mode, that the strip is built, that no two
faces overlap and that it has 6n, 4n+2 or 4n+2 faces; and that the face-perfect strip with its
walls deleted coincides, face by face, with the strip stamped directly.

## Citing

If you use this application, please cite the paper:

> E. Andres, G. Largeteau-Skapin. *Introducing Factory-Nets.* [venue, year, DOI to be added]

## License

MIT, see [LICENSE](LICENSE).

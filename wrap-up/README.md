# Wrap Up

Last, it's worth noting that images are composed of layers where each directive
in your `Dockerfile` creates a layer. These layers get cached by Docker. There
are three important implications to this.

1. Docker shares layers across images for efficient use of disk space. For
   example, if our own image were based on (`FROM`) `ubuntu:18.04`, all of the
   layers that comprise `ubuntu:18.04` are _also_ layers of our image. An
   implementation detail-- they appear on disk only once. This is also important
   when pushing or pulling images. Layers that are already present at the
   destination are reused instead of be transported over the network
   unnecessarily.

1. Comparing to a cake, you cannot possibly add a third layer to a cake that
   already has two layers and expect to end up with a smaller cake. The same is
   true with Docker images. Even if a layer deletes files from a previous layer,
   the net size of the image on disk can only _grow_ as layers are added. This
   means that managing the net size of an image typically involves minimizing
   the incremental size increase added by each layer. For example, if a system
   package is needed to complete some step, such as compiling something, and
   then never needed again afterwards, it is advisable to install the package,
   compile the code, and uninstall the package all using a single `RUN`
   directive to execute a script (often inline). This will minimize the net
   increase in image size contributed by the associated layer. _This is an
   advanced topic._

1. Docker _caches_ layers. When you rebuild a `Dockerfile`, layers that are
   unchanged (because the associated directive's inputs _and_ all previous
   layers are also unchanged) simply get re-used. This means that rebuilding any
   given `Dockerfile` is usually faster than the initial build. Advanced users
   take advantage of this caching by organizing their `Dockerfile` with the most
   time/compute-intensive directives (installing packages, for instance) toward
   the top (lower layers) and directives whose inputs are more likely to change
   (compiling source code, for instance) toward the bottom. This strategy can
   help ensure re-builds are fast. This also is an advanced topic.

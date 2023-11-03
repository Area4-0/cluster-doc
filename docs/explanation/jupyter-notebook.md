# Jupyter notebooks

TODO

## Launch a Jupyter notebook server inside of the container

You can launch a Jupyter notebook inside of your custom container, to make it available from the outside you have to specify some additional parameters like the following ones:

```bash
python3 -m jupyter notebook --ip 0.0.0.0 --allow-root
```    
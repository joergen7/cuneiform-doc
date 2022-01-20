# Cuneiform Documentation

###### The source code for the Cuneiform website

## System Requirements

- [Python 3](https://www.python.org/)
- [Virtualenv](https://virtualenv.pypa.io/)
- [Sphinx](https://www.sphinx-doc.org/en/master/) Python documentation generator
- [GNU Make](https://www.gnu.org/software/make/) build system

## Prepare a Virtual Environment

In the `cuneiform-doc` directory run

    virtualenv venv

This creates a directory `venv` that holds the virtual environment's data. To enter the virtual environment run

    source venv/bin/activate

We can see that we are inside the virtual environment because the shell prompt has a `(venv)` prefix. Now, install the necessary software.

    pip3 install sphinx

To leave the virtual environment run

    deactivate
	
## Build

Enter the previously prepared virutal environment by sourcing its `activate` script

    source venv/bin/activate
	
Build the static HTML site by entering

    make html
	
Leave

	deactivate

## Resources

- [cuneiform-lang.org](https://www.cuneiform-lang.org/). Official website of the Cuneiform programming language.
- [joergen7/cuneiform](https://github.com/joergen7/cuneiform). GitHub repository of Cuneiform.

## Authors

- Jörgen Brandt ([@joergen7](https://github.com/joergen7/)) [joergen.brandt@onlinehome.de](mailto:joergen.brandt@onlinehome.de)

## License

[Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0.html)

To build:

1. Install git
2. Install python 2.7 - http://www.python.org/downloads
3. Install pip (optional - Python 2.7.9 comes with pip)
    1. Download: https://bootstrap.pypa.io/get-pip.py
    2. Run `python get-pip.py`
4. Install sphinx - `pip install sphinx`
5. Install readthedocs theme:  https://github.com/snide/sphinx_rtd_theme
6. Install rst2pdf: `pip install rst2pdf`
7. Clone this repository: `git clone http://as-codehub-ci.cisco.com/mtimm/aci-troubleshooting-book.git`
8. Cd into the aci-troubleshooting-book directory
9. Run `make html`

To test a build:

1. Cd into the build/html directory
2. Run `python -m SimpleHTTPServer 8000`
3. Open a browser and browse to http://localhost:8000

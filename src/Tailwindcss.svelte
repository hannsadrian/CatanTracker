<style global>
    @tailwind base;
    @tailwind components;

    input[type=range] {
  width: 100%;
  margin: 5.2px 0;
  background-color: transparent;
  -webkit-appearance: none;
}
input[type=range]:focus {
  outline: none;
}
input[type=range]::-webkit-slider-runnable-track {
  background: #969696;
  border: 0;
  border-radius: 1.3px;
  width: 100%;
  height: 5.6px;
  cursor: pointer;
}
input[type=range]::-webkit-slider-thumb {
  margin-top: -5.2px;
  width: 16px;
  height: 16px;
  background: #ffffff;
  border: 1px solid #000000;
  border-radius: 34px;
  cursor: pointer;
  -webkit-appearance: none;
}
input[type=range]:focus::-webkit-slider-runnable-track {
  background: #a3a3a3;
}
input[type=range]::-moz-range-track {
  background: #969696;
  border: 0;
  border-radius: 1.3px;
  width: 100%;
  height: 5.6px;
  cursor: pointer;
}
input[type=range]::-moz-range-thumb {
  width: 16px;
  height: 16px;
  background: #ffffff;
  border: 1px solid #000000;
  border-radius: 34px;
  cursor: pointer;
}
input[type=range]::-ms-track {
  background: transparent;
  border-color: transparent;
  border-width: 6.2px 0;
  color: transparent;
  width: 100%;
  height: 5.6px;
  cursor: pointer;
}
input[type=range]::-ms-fill-lower {
  background: #898989;
  border: 0;
  border-radius: 2.6px;
}
input[type=range]::-ms-fill-upper {
  background: #969696;
  border: 0;
  border-radius: 2.6px;
}
input[type=range]::-ms-thumb {
  width: 16px;
  height: 16px;
  background: #ffffff;
  border: 1px solid #000000;
  border-radius: 34px;
  cursor: pointer;
  margin-top: 0px;
  /*Needed to keep the Edge thumb centred*/
}
input[type=range]:focus::-ms-fill-lower {
  background: #969696;
}
input[type=range]:focus::-ms-fill-upper {
  background: #a3a3a3;
}
/*TODO: Use one of the selectors from https://stackoverflow.com/a/20541859/7077589 and figure out
how to remove the virtical space around the range input in IE*/
@supports (-ms-ime-align:auto) {
  /* Pre-Chromium Edge only styles, selector taken from hhttps://stackoverflow.com/a/32202953/7077589 */
  input[type=range] {
    margin: 0;
    /*Edge starts the margin from the thumb, not the track as other browsers do*/
  }
}


    @tailwind utilities;
</style>

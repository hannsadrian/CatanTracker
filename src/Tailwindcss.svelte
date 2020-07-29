<style global>
    @tailwind base;
    @tailwind components;

    input[type=range] {
        width: 100%;
        margin: 15.8px 0;
        background-color: transparent;
        -webkit-appearance: none;
    }

    input[type=range]:focus {
        outline: none;
    }

    input[type=range]::-webkit-slider-runnable-track {
        background: #d2d2d2;
        border: 2px solid #010101;
        border-radius: 5px;
        width: 100%;
        height: 8.4px;
        cursor: pointer;
    }

    input[type=range]::-webkit-slider-thumb {
        margin-top: -16px;
        width: 15px;
        height: 40px;
        background: #ffffff;
        border: 1px solid #000000;
        border-radius: 18px;
        cursor: pointer;
        -webkit-appearance: none;
    }

    input[type=range]:focus::-webkit-slider-runnable-track {
        background: #dfdfdf;
    }

    input[type=range]::-moz-range-track {
        background: #d2d2d2;
        border: 0.2px solid #010101;
        border-radius: 5px;
        width: 100%;
        height: 8.4px;
        cursor: pointer;
    }

    input[type=range]::-moz-range-thumb {
        width: 15px;
        height: 40px;
        background: #ffffff;
        border: 1px solid #000000;
        border-radius: 18px;
        cursor: pointer;
    }

    input[type=range]::-ms-track {
        background: transparent;
        border-color: transparent;
        border-width: 16.8px 0;
        color: transparent;
        width: 100%;
        height: 8.4px;
        cursor: pointer;
    }

    input[type=range]::-ms-fill-lower {
        background: #c5c5c5;
        border: 0.2px solid #010101;
        border-radius: 2.6px;
    }

    input[type=range]::-ms-fill-upper {
        background: #d2d2d2;
        border: 0.2px solid #010101;
        border-radius: 2.6px;
    }

    input[type=range]::-ms-thumb {
        width: 15px;
        height: 40px;
        background: #ffffff;
        border: 1px solid #000000;
        border-radius: 18px;
        cursor: pointer;
        margin-top: 0px;
        /*Needed to keep the Edge thumb centred*/
    }

    input[type=range]:focus::-ms-fill-lower {
        background: #d2d2d2;
    }

    input[type=range]:focus::-ms-fill-upper {
        background: #dfdfdf;
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

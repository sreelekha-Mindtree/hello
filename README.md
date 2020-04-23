import pdfMake from 'pdfmake/build/pdfmake';
import pdfFonts from 'pdfmake/build/vfs_fonts';
pdfMake.vfs = pdfFonts.pdfMake.vfs;

docDef = {
    content: [
      {
        columns: [
          {
            image:
            "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA9gAAADACAYAAAD/R8saAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAEnQAABJ0Ad5mH3gAADIJSURBVHhe7d0/rC3Fle9xQgIkhMa6WBb+A5ZHT7ZkIUfjiMg4cESCkEgInvWQk0neOHFm4pHzx+RYznytycAvAxJAspAsjSxDggPriRmZJ2MwvPv4nUNz++y7eu+uqrWqVnd/l/SR7Ms5p3r3rt27fl3V3ff9t//5X3cAAAAAAEAbAjYAAAAAAA4I2AAAAAAAOCBgAwAAAADggIANAAAAAIADAjYAAAAAAA4I2AAAAAAAOCBgAwAAAADggIANAAAAAIADAjYAAAAAAA4I2AAAAAAAOCBgAwAAAADggIANAAAAAIADAjYAAAAAAA4I2AAAAAAAOCBgAwAAAADggIANAAAAAIADAjYAAAAAAA4I2AAAAAAAOCBgAwAAAADggIANAAAAAIADAvbO/eu/f3jnxd/+zZ3+rtUeAAAAABwVAXvn/vSfn96JKP1dqz0AAAAAOCoC9s4RsAEAAACgDwL2zhGwAaC/n/3qr1es/wYAAPaLgL1zBGwAiKUg/ep//P3Oe+8vH2/13/QzhG4AAPbtcAFbN+h6+e2PrwY6kz/++dOrwc9kGgydevOdT65+V39jK4MkAjYAxND3wO/f++Tzo+L60u8QtIFxHn3u9Ttfe/r2na/86MUrD33v+Rvuf/jxOw9+55kv/v+Xvv/TL35W9Pvyj//8J/PvAzi2XQdsDWBuv/HxVTD+Px/8v8+HNr6lv6u//9KrH9357y/+X3M7RiJgA4C/f/vff7vz0d8/PyBWlH73l699ZP5tAH6++ePf3XnkqZfu3HrihavQfN9997nS3/zyD35x5xvPvkLgBnBldwFbQVcz0i0Dn5bSTLdmubPMThCwAcCXgrFX/ebNj802ANT71k/+cBWqH3jsh2YojqQ2FeY1Q25tG4D920XAVpjVUu+/fBgzS11bCvoK/NY290LABgA///rvH7qfwNXftNoCsJ5mjxWqI2apa2mpuZaUM7MNHMumA7aW6CnEZi8Ff50AGLGEnIANAH60Ssm79B1htQXgMoVXhViFWSvkZqBt06y2Ztat1wBgXzYZsHW2P+qa6sjSrIeuCbdeUxQCNgD40EndqGKpOFBmC8HaohumPfrca+ZrArAPmwrYmgHWDcW2Xpqt0EDNeo3eCNgA4CNyxZROGlttAriXrm/eWrA+pRujWa8NwPZtJmArkGa7xrq19KiW6GXjBGwA8BFdGZ9EAWSiWWs9NssKrFuk68V1l3PrtQLYrvQBey+z1kulWYvIG9wQsAGgXeTy8Kl6rWwCtkjLqrc+a23Ra/rq0782XzOAbUodsBWut3itdWnp2uyo6+8I2ADQrkfAfu0//m62DRydllNb4XRPdG02dxtHVo8+93qIva7gSBuwjxKu5xURsgnYANDulbc//vzoF1cEbOAmBc5Mj92Kpmdoc6dxZGT1Vw8Pfe9/mO1tXcqArSXTe7veem15h2wCNgC0++VrH31+9IsrAjZw19HC9USvmZlsZGP1VQ8E7E4UrrVk+silZ2Zb+6YGARsA2vVYIs6juoBrRw3XE0I2srH6qQcCdgeE67ul5YjWPipFwAaAdj/71V8/P/rFVeQNL4GtOHq4nmgfWPsHGMHqox4I2B0c7ZrrS+Ux2CJgA4CPyO8onVy22gSOhHB9060nXjD3E9Cb1T89ELCD6doz6mbpOvTW56ISsAHAR+T31O/f+8RsEzgS3UnbGoQfGSEbGVh90wMBO5Bmaim7/vjntiBLwAYAHzrhGXUZk5agW20CR/HIUy+ZA3Dcd+frz75s7jOgF6tfeiBgB2Jp+PlqufENARsA/EQ8ruutd5m9xrHpWbjW4BvX9PgubnqGkax+6YGAHYSl4ZerZak4ARsAfGk5t1e1rlICtk7BUQHSGnzjrq/86H+Z+w/oweqTHgjYASKX25WUZtAVGC1ZZtdrn4+q1xBR+rtWewCwd/ru8gjZCtet99kAti7jddca9D/47Vw3W7v/4cfvfOsnfzD3IRDN6pMeCNgBtPR5RGlQo2V+eq6ptV0WXR/3y9c+ulrK98GH/UO3TkTUDMQI2AAQQ98jNSeJ9Tu1J02BPXn0udfMQXcP99/67p1bT/z86vpmbcel8Kr//tWnf33nyz/4xbDwrZMR1rYB0az+6IGAHaDn7LBCsQK912yBwrmCes+quU6PgA0AcfSdorC85sSrfkY/y6w1cG3EI7mmUG1tTwkFboVtBXWrnSg6GWBtDxDJ6oseCNjONCPcqyJnCnQH9F4z2pr1sLbhHAI2APSh7zWdfNV3zpz+jbuEAzdpNtgacEfRQF43U7O2pYWuIe95B3Rdr25tBxDJ6oseCNjOIu7EeloKpArAVvueNBvhedObc6Vl6tY2LCFgAwCATHre2EwzzArA1nZ4Unh/4LEnzW3wFnGiADjH6oceCNjOopeH9wrXcz1CdukdZwnYAAAgE90R2xpse9O10j1vDKYTBz2uz9Yyd6t9IIrVDz0QsB31WB7e8uzoFlGBdl4lSw0J2AAAIAuFUN0R2xpse9LM9YiZXgX66Ouytf+stoEoVj/0QMB2pOvRImtk+NNy8Zq7ypZUyTJxAjYAAMiix7XXo8L1RG1b2+XJ40ZtwFpWH/RAwHYU/Xiu0uuUvemmNpGlv2+1a8kcsHUy4sXf/u3K7Tc+/uJ/C3fZvZcueZjvI+2zl179iH0WZKl/crOqetp31j6l7+7X0nsu1s8fzfw48/LbxzjO9LhzeIZrlLWM29o2L1tZJq4VC48+9/oNuib+G8++cuPfrN/FZerr0z6d70/td+vna1l90AMB21FkAK2507Y3fWFGzmKXhNssAVtBUNeov/f+p8X7Rtfrv/nOJ1d/4wgDcQ2s9Fpf/exzUrO/VNpn+l3t86Pst1raNxr4T/2zpPTzov7Z+54PmakPKyzonhEl99tQX5/2qX5/zyFjb9T/p2OWlJZ+R7+/18/RdJzRZ0Kv9S8FTx+Zjud7+Ez0mNnV9d1W271pqbi1fZ68Q1QrBbuv/OjFq+d1P/S9581tXkMnYfQINIXwntfQZ6dHtJXs2/l+tP5eCevveyBgO4oM2B4zqx6ib3hmtWkZFbDnocX7ZIMGGxqI7WnwrUGlQlrJoKu0pgFatgHsvwVcMrK2f3o/y17vX4awHXGMvbRyZgrVJYF6TenvZQkWEX11Kv1tq81Lor5PrbZORR239J2hz6Y+o1a7WzH6OKPVfN5V208n0bO6WhqeKXRGv14tt7fa7UXhV4G6JUyvoTvOK1h+7enbw99fhVxrG1stnRjS69XsdOtd9/X708oO679vTfZgPiRgR4U+1VvvfmK22Vv0Mvi1A/jeAVuD4OiTC/NSW1sN2hp8RYfqpdIANsu+iwgt2qdWW3q9NbNrNTUNgvU+W9sSKSJ0qb9Yben969WHp7BtbUcPEX11qtrg0jtgqz/rBGev91ztbC1oK9h6h+qlOrd/IvpGbT8VBYXom5uNDpynomex/+Gf/sVsN9IU+Hos9beoD2lWdtTMdq+Arf1864kXzJ+tpW3X37b+29YQsA2RAfvSLEsvGshH1tovuZ4BW4Mu79nqtaXB/4ggU2MaoI7aV6c1KgRO1Jcjat7GtM9HlN7n3veFiBhYn37mdYzrFSJOS0F7xCqBqL6qqg0uPQO2+nGvYH1aWwjaPU/gnZbaPf1MZAvY0Tc30+OxrHZHi3xsl2YlrTYjKNB6B75WmtWeQmMvPQK22og4GUXA7oeAHSiy1n7J9QjY2pZRg655Kci0fPlHyxas56Vt0raNCNp6zyJq+vsjQ8G8NADutWIgOmBn6ce9Tw5F9VVV7bErKmDPt2dkcDytrCdTtbIi22ci4gRYy3esZlutgbKXrHfV1myvtb1erDY9ZQzWpxS0ey0djw7Ykf2FgN3P7gL20jLGESK/bNfOiEUGbH2Jj5rBOlejnoF+jt6vjMH6tKagbb2GKFGhRX83SyiYSvu3xxLniNClbdcMWYaTFfPS9rQM+ktE9VVV7WuIDtijVn6cK61gyBKy9Znwvu9Aa+mzqu/BiO//ls9a5PJwXXtttZlB9I3dptAUQWEvelm/F21nj5MsUQFbgVEnCqz/5oWA3c/uAra+6Kw2R4h8nWtn6qO2QYPabIOKefUOiUs0CNRJn61VzwFsVGjJfEJDwT9y/0aFrsz7VDN31r7wdKSArZOCmY/x2rYRlwnMRd9rpbUiPq+1/TQ6ZGZ/ZNUDjz1pbreHiOvONWsdfeOyKLo+O3I2Oypg90DA7md3AVs1+kt3sueAvYUavZpBA5Fss30lpW3v8VmKDC2ZS6s/rP3hISp0Za9XglcHHClgZz6ZMpW2sddlF6eyh+uoqu2n0cukI2dxPSgMWNvtQYHSarOWAvtWZq2X6AZsUSGbgJ0DAdsQPfiLHLiWIGCPr7VL6b3tZfClAWztgGqtowZsVdRJoKMGbFXkJSJHCthbKa0GsfZLpKOGa1VtP428/lqzw1abmej6WmvbPXgGjegTIT1FhWwCdg4EbINCT3RFDrLW0jZo8BNh7Zfc0QO2AmLva/X2OPjaamjZQkWEbB0jjlxR/ZWAnbO0D6x9E2GPx/eSqu2nkTOi3jO4ESLvoK59a7VZKvuNzGpEhGwCdg4EbIOWdEVXj5m3LTh6wFb1nOHY8+Ararb16AFb5b1vCV0xIZuAnbd6XM5y9HCtqumn0YEk693D56L3QWuI3GO4nniHbAJ2DgTsBb2u74qaydgKAvZ1RV+bKUcYfEXsRwL2dXnOwhG6rqs2tC4hYOet6Buc9lh5t4Wq6afRz7/WDbmsdrOxtt3LFJxqRL8/GeiGbdZrr0HAzoGAvUAzNr1K12RneaRHbwTs69IJHWv/eDlSSNxSaNlaed2widB1XbpRn7V/akX21drPFe/13Yq654bGD1u+YaVn1fTTyOuPxWozI2vbvdQGbM3+W39vj1pOQswRsHMgYC/ofTZYAavH82ezIWDfrajVDBp89VqRkaH0Wj3v3EvAvltelzMQuu6W9oW1j2oQsHNX1OVAb727vUctRlVNP428wVn2QfacZop1siFCTXjUsumt3y28xAOP/dDcD6UI2DkQsM8YEUp0Fvr2G8cJ2gTsuxU1+Mr8rNio8nxONgH7ZnnMwhG67pbnCSECdv7yfmwXx6ebVdNPNRC2BsgetnCDs6y+9P2fmvt0z3QywtoXJQjYORCwz+i5TPy0NOh69bOByd6XjhOwb5b3jXCOPLPhdWMuBrA3SycBW49LhK6b5fXoRgJ2/tIx2dpPtVgafrNq+qk1OPaix0pZbeK8Iy0Nn9OMfesNzwjYORCwz8iytFaDr5deHfO85GgE7JvlebdmhfWjl8dNzwjY91ZrSCB03VseKwMI2PlLYwqvE+fs23urtJ8qzFiDYy9TYEAZLZe29ucR3Hri5+Y+WYuAnQMB+4JMX2A6U/3mO590edxHLwTsm6XBl7WfamjJ+dHLYzBLwLarZakrweDe0vHd2lclCNjbqNp9OccJVLtK9210GCFgl9tyQPTQei02ATsHAvYFWWaxT2svYZuAfW95vKcjH8mlz4ve17mRnyEN8K19tBYB266WWWxCl12ts9gE7G1U6zFJRl7ClrmyBWzP5xsfhR5ZZe3LCA889uTVdc9akq6+cPp+6f/rv+ln9LPW34jwzR//7sZ2lCBg50DAXqH3HcVLS+FFX7ZbXEY+MmCrbQ109IVsfSlrhk5BVUGiZ0BsvZu4Tgr1vi5PlzGs2W79jH62Z+m9a5nFjgwtl0p9VMvcrT6q/ql/0z4d8TnSfp1vT4mRoUvHSu0z7bvTk1n6//p37fMPBlzb2nottrY9qk7731oj32u9h2pf3+Ha/tPjgP6//l0/0/MzpLbm21FK2z2ipuO89tl8Bcu0H6d9OfLGmtqG+b66JDqMWG1imZ4Zbu1HbwrLumu6tQ3n6Hd6BO2Wm+PtIWDXsP6eh+xBuVaKgC29Q0FtbS1s9w4G2j8KzDXLWzWw6BG0W6/D7jmg1b6sCa/6Hf1ur9I+sbZjDQ3YetYUCkr7qH6+53uvqp1x7b2dGvDr81vaVxW4ex/7az5Pk8i+WhpcJr3fa5W+V2r6Zq/3u+XklKgv9yptq0441Xx2ep+cVpX2U81MWoNqL1abWKabwln70VPrjec0q/3gt58x/7aXB7/zjNn2GgRsXwTsYPpyGTGj0VL6YlNYqx0Y9dB71qBl8CoKMdFn5/X3rbbX6jF7rc+CR7/S3+jxudJnofa91zb2Kg3uW/uoBra9ZpC0vdY2XNIzdKktaxtKKKz1CgotN+aL7Ku1n/ee77XeI/V/aztK6Hszulq2s9fnW9+ZNSej53Q867W9qtJ+SsDOJfKZ5FIza21RyI6eydZsvtX2JVkCtoKp6KZt+pxN9B7r362TFATsftIEbNEXYu+zsV6l0KXHfrV+WXrrFbB1Jt1qv4YGDNH9oDZk9bicQYOl1hA412sAVhu0egVsjyA40T7tNfNa0xd6hC59Rmtn2C06dvY4GaTPgtX+GkcO2Npvnt9v0Z8fzUJb7V6icUiPal1JdarXiqVMAfv+W98128QyPabK2pcevJ9JruukrXa81J4MGBWwFZi1OqD0vgP6eW2zfrf2pIJY2+SBgN3JlkP2VBo41A6WvPUI2LUDmXOig2zt+xN953D1/YiTNApp0eFF214TBiNDy1QRfbTXiYuaGdfo0KX32mMm81Sv43/ttkf21dpjUo+A7bHy45T+XmTVnlDrMbvuHa4nPZa2l/bTyIC914F5JGs/eog62RE5466+abV5Se+ArRnqlmDsxdo2DwTsjnrMEvYoDb5vv+E/sC8RHbA9Z65PRQbCmpk3Bd/Iigotkx7hpWa/RgfsqMGsKCRE79OaGdfo0BVxwmIS3R9UtcetyG0rDS6T6Pdax2HvcD2JDLM1n/usn+cS0SsDSvspATuPyBlhBWGrzVa6w7jVnofaGfdeAVsnLbyW3HuwttEDAbuzXjMZPUrLx0cF7ciAHT1QiFzyVjO7Eb0Er3bGpUT0DEfNoDYytESGg0mPE4KlryEydGkAb7XpKfqzVnvsOmLArt2uNSI/O/rus9o8p8dnOfoyMh0rIk9Ol/YHAnYekcGwdjZ4Das9D7X9p0fA1vXnLY8Si2BtpwcC9gAK2dHLWnuWgnbkYMUSFbCjZ1slcjBbE2Yjb26mfm61GUHhIqrUL6w2z4l8n2tm1GtErxQpPW5Ehq7oExbSYybRaveSyL5a+90Q+V7XHCdLRVVNwN7DSVSJPFFQ2k8J2HlEBkP9batND3qfrTZbZQ3YmrnOsCT8lLWtHgjYg2igFT147V26jjc6nE6i9l3N4KWU3vuoKh3oRC8P7xUEJTIkqEr7dsbQUip6n5b218jQZbUXIfI1qGr6Rsa+uvX3OuqEX80qhcixhk4Y9Tg5JZn6KQE7DwL2Tbrhm9XeJdEBu/UxZ1GsbfVAwB4serA1onTXceu1etpywJaoKl3mqhtNRVX0UntL5HV6pWEwY2ipETk4L+2vewjY0bPYNTePy9hXt/5eR35urPbOiazS42KLTP2UgJ2Hlhxrn0WIXM6sa6Wt99+D1d4lkQFbdwq32szA2l4P6j9We1u3mYAtmhmLXN46ovR6Imeztx6woy4RKN3+yEDa8lzeWpHXYpeeMMgYWmpE7lNdnmC1uWQPAVuy3QQrY1/d+nsduSzbam+JvocjK/ra67lM/ZSAjVaRfchq75LIgK2bulltZmBtrwcCdiIaUERfn9ez9Fqi7sq79YCdZfsjq+fAay7yM1TymjKGlhqRlzSoSpaX7iVgR15LWrNyJGNf3fp7nWX7M510bJWpnxKw0epIATtyqX0ra3s9ELCT0WAzcnZjRNXMqFxCwLarZPsjByu9B15zkZ+fkkFYpsFgq8iVDiWvZS8BWyJPBFntnZOxrxKwl8tqb0nk8bD3KqVM/ZSAjVYE7Bys7fVAwE5Ky7oiB7W9S1/ynjdCIWDbVbL9kbNoGlxabfaQ5XVlDC21ImfBSvbp1kPXXJYTQZKxr279vc6y/TrZGVWRl4FZMvVTAvYxPfrc63e+9vTtz97/F6986fs//ez9ev4G6z3tzdr2SwjYvgjYyWlJauRArGfpi94rZBOw7SrZ/sgBYO2g2kPkkuaSMJgxtNSKfC0lNzrbU8COfC2lM4sZ++rW3+ss2x9ZVnuRMvVTAva+6XFS33j2lS9C9AOP/dB8r7KyXtMlBGxfBOyNUNDWF/bWr9HWo7ys11eKgG1XyfZHrpAYdf31JOpzUrJ/M4aWFlFVsk/3FLAj+4f2k9Xmkox9lYC9XFZ7S6Kq13flXKZ+SsDeH4VqPUrqwe88Y74vW2K9vksI2L4I2Buk5ZpRAa1HaUbeel0lol5/r0FDhu2PXDpotddThv2bMbS0yHDn+z0FbJ2EiioC9vmy2vOWYfsj+5jH93ipTP2UgL0P//jPf7pa8r2HUD1nvdZLCNi+CNgbpi9PPQokauAbWaUDwFMZAlSLDNsfVb324TkZBrcZQ0uLDH1266HrVFSVHl8z9tWtv9d7PwaV9jEPmfppZMAWq034UbC+9cQL5r7fA+s1X0LA9kXA3gnd2GlrYbt24CUZBvstMmx/VI2Y2Tila1CjymrPkmkw6CEqMJQ8C3vroetU1HGg9DOYsa8SsJfLas+yt2NQptdDwN4uXVd9/8OPm/t9L6zXfQkB2xcBe4d0Z88thG0NrGtvekbAtitDwB4xs3Eqw0As02DQQ4bAQMBeV6XHsYx9lYC9XFZ7lr0dgzK9HgL29nz92Zc3d7OyWtbrv4SA7YuAvXPZw7a2zdruS7IMTGuN3v7IgQoB+1qmwaAHAra/LMexjH2VgL1cVnuWyMfrjTgGZeqnkWFErDZRR8vBszw+qxdrP1xCwPZFwD6QrGG75o7TWQamtUZvf+RAhYB9LdNg0AMB21+W41jGvkrAXi6rPcvePi+Z+ikBexsUrvd2A7M1rH1xCQHbFwH7oBS2dZ1ehsd+1Vyzm2VgWmv09kcOVDSos9rsKcNALNNg0IPu8xBVay8V2Vtg0AnPiNITAqz2lmTsqwTs5bLasxCw11dpP40O2N/88e/MdrGe9uERw7VY++MSArYvAjaGP/ZLIb/0WmwCtl0ZAnbtgNpT5ONp1r6+ve3jDK9nb4Ehy+vJ2FcJ2MtltWchYK+v0n6q8GYNqr1kDiRboPdn7zcyO8faJ5cQsH0RsPEFfcGMCtq667O1TUsI2HYRsK9Fvj4NWq02T+1tH0fOYK99PXsLDFEz2CqrvSUZ+yoBe7ms9iwE7PVV00+tQbUX3UTNahOXHT1ci7VfLiFg+yJg4x6a/fvjn/sG7dIljQRsuwjY1yJfn4Km1eapve3jyMH62tezt8AQdRxQWe0tydhXCdjLZbVnIWCvr5p++sBjT5oDaw9f/sEvzDZx2VGXhc9Z++USArYvAjYWKUj0vCFayc3OCNh2rd1+XYMfVWsDaKQMA7Fsg8FWBAZ/WY5jGfsqAXu5rPYsBOz1VdNPNYC2BtYetjQ414zxo8+9HuJbP/mD2eaS6MenbYW1by4hYPsiYOMsXRutm5D1qJJl4lkGprUybH9UaVBntddThoFYtsFgKwKDvyzHsYx9devvdYbtj3xfrfaiZeunkWFOS5ytNjOKnDHWs6utNi3R18VvibV/LiFg+yJgY5UeIbtkUJhlYForw/ZHFQH7WrbBYCsCtr8sx7GMfZWAvVxWe5bI99VqL1q2fvrVp39tDqy96BFTVrvZWNvupSSYsTT8Lmv/XELA9kXAbqBltu+9/2kY/X2r3VF0nXRk/eXD9ddhZxmY1sqw/VGVIWBHDm7XDsSyDQZbZQgMWw9dp7IcxzL21a2/1xm2f2/HoGyvJzKQSOZQMomeNdbft9o9FX2yw3L/re9ehSitZFD7er9K3rPIFRBWe5dE9ufMfdnaXg8E7AaRB3vViC+wcyKv253KateSZWBaK8P2R50w0Z2RrfZ6irw789pHymUbDLaK6rMlNzjcW8COqtLPYMa+SsBeLqs9y96OQdlej2aYrYG1ly3c6ExLuK1t92K1aek1e61QrfelZOn6EgJ2Dtb2eiBgN4g82KtGfIFdEn138bWvmYBtV8n2b30fnhP12lRWe5Zsg8FWWmESUSX9ZU8BO/JZ7dpPVptLMvZVAvZyWe0tiarfvFn2aE0PGfvpg9+OC3YPPPZDs81MIkOi9q3V5indCM36fU8K1nqtnsv2Cdg5WNvrgYDdQDNZkTViEH2JvlQja+1r3no4zLD9Udvw0WfjSqu9nrQNEVUy25pxMNgiqkr67J4CdmT/IGCfL6s9b3sP2CNWKmXsp5rNtAbXXtYukR5FIcLabg+3nvi52eapR556yfx9L3ocW8T7QMDOwdpeDwTsRpFVe8CPFH1SYe3AMENAbZFh+yNXI5Q8ci1CVJXs34yDwVqRr6Vkn+4pYEe+lrXH0UnGvrr19zrL9kedbOz1XTmXsZ9GhhJRCLPazUKz7NZ2e1j72iOXh2sWPepmcwTsHKzt9UDAbhRZJY+t6imy1g4MMwTUFhm2X/0rqmoHKx4iB2ElwSXjYLCWnm0eVSUzYVsPXXOR9wkofRZ9xr5KwF4uq70lUd81I1YqZT2mWoNrLwqPVpsZRN/gbE0oi14eHrmCgICdg7W9HgjYjaLODqtKBvM9RX1hq9a+5gwBtUWG7Y+8ad2I5YOTyOBSct1h1sFgjSz7dE8BO/KpDKUrSDL2VQL2clntLYncjt4rlbIeUyOXSUvWZeLRS7MVnq125yLvHh59kzkCdg7W9nogYDeKDJsl13v2FPmaCdhtVbr9USeISh655i3qZlyqkkFY1sFgjch9WvI4wr0E7MgbnNXMLGbsqwTs5bLaWxK5+mTt97WXrMfU6KD50PeeN9sdLfrO3VabpyJDavSJDQJ2Dtb2eiBgN4q+q/baRwL1FDnYJmC3Ven2R/bfEc9xj5yVLw0uWQeDpaIfz2e1uWQvATvy8oyaY1jGvkrAXi6rvSWRJ3N6n0jNekztcRfrbAEl+jWvDSdRIXXtHcxbELBzsLbXAwG7UeRASTXiURiXRNbaLzkCtl2l2x85CByxTDzy86iTEVabS7IOBktF9pFM/dVqL0rU51+lfWS1eU7Gvrr19zrT9kdeytbzRGrmY2r0MvFss9i6w7e1nV60KsBq91TUfu8RjgjYOVjb64GA3SjygK8audTWEj2btfZLLktArZVl+yP7rwZ1vVdgRK6uKL3pYObBYInIfVp6EmYPATtyRlFVeoMzydhXCdjLZbV3TuQJnd+/1+9EauZjauS1wJOvP/uy2XZvPWbs11x/LVEBe+0jwloQsHOwttcDAdtBdOmL2mp3hMibHanW3jSFgG1XzfZHVs++GzmgVZXe0CfzYHCt6Ofel67Q2XroEgWSyCrtp5Kxr279vc60/dmOjbWyH1Pvv/Vdc6Dt5f6HHw97ZFSJ6NnrkmAS9ZgwZrB9EbD3o2vAjjw7rBoxE2jRNkTOZqmsdi0EbLtqtj+6//YYfKlvRi6D/KBiJUnkYFADZqtNb9Gf99K+ERkUPAbYl+j1RlZNP5WMwYWAvVxWe+dE3uhM9d77fb431U5UeXz+dddpa6DtSTcWGxmyNYtubZcnrQaw2rZYv+9Bwd1qz4veQ50wsdr2YLV5CQHbFwHbQfR12CrdUXx0yI6evVZZ7VoI2HbVbH/0LGXptcs1ovtmTaCNDC2q6EAYGRBUNWEwcpt6nMiMDAiq2uW6BGx/mbY/+gSkKvp4FD3O8tj+HkunZdT12LqrdmQonJScQLB+30vkiQy9h1abXqw2LyFg+yJgO9CXV48aGbKjQ5iqJIgRsO2q3f7owVfp9cslevTNbMtuVZpdjjoe6F4L0X2i5iZ40aE/8mRQj35ac/21ELD9Zdv+6EsTdLyIuuFZ9L1fVF4nCP7hn/7FHGx7u/XEC11nsnXyoEe41v6z2l+iEGP9HQ9R17xHLg2fWO1ectSA/cBjT5rb3IqA7ST6y2sqDaq9vgjW6jEwVKkdq30LAduu2u2PDi6qkvd3regQq6oNXT22Tccd75DdI1yrak5a9OinLwecDOpxDK1dHi6RfbX2+4qAvVxWe5f0CKk6bnhfEqT+0+N4VNtPT/WaxRYtY45+VrMoaPYI11IaaiMDtvav50kM/S2dGLHa8ma1f8lRA3ZUH9Jnxmpv67oH7B6D6Xlp0B89m62//+Y7fU4cqEpeDwHbrtrt177vMYjxDC+areuxzRlnBeellS1eg1r9Hf296FIbVvuX9AjYKs8TF70CQs2KgElkX60NLgTs5bLaW0MnYaJLkwBeM9n6vuhVtf3U0uNa7Lmv/OhFczta6WTBl77/U7PNCJpJtLbjnOgbrun1W+2W0okQXT9vtRHB2oZLCNj+1t4Nf0u6B2zpMTA9LQ0EX3q1LgAs0cDy9hsfh9/gaF6ls4QEbLtatr/XKgxdh9oSCNU/e21r1lnB01KAax0gajDbIwiqalcz9ArYqtYTF+qnPU9QtmxrZF+t7ZcE7OWy2lujx/1ipnr1s9dvbcMa6ssaE/Ss1uPnnGYqo+8ofkqzrQr2HjPaX3v69mehI/YaYUvNkuwey611AqN2Jlu/p9/vtQJgYm3LJQRsfz0e99bbkIDdc0B9WgrDCh0aJL/42/IvCv2OQnXvL7WpSgfcBGy7WrZfg5pepSCn8FEy06HtU//ueeKnZVn7iOOBQqE+xyWzrzpB1/Nzr/e+dna4Z8CeSvum5CTmdIKy5wnX1uNWZF/V37bavISAvVxWe2uob/YsHatLjvP63ETfCHCpavvpkh7Bb8kUth997vUr52bR9N8VqBUCFap7B8FJ7fWqPe5qLtov2k/WNlgUKHstB7dY23TJUQN29H0T1pygmT6H6jP6/GbeX0MCtvSaWVtTGuDpy2qibdOX3fzfRsy6W1U64CZg29W6/SP67zQI04yHTvTMKVDr30f0U7Vp7aO1IkPLpVKIVTDUvrP2q/5N73WvGet5qV1rf60xImBPNZ3E1L6bTmROFMD171s5QXmKgO0v6/aPOMarpvHIdKyfjkFZxiHeAVuibp60Ry1Laa2/F0XhRyciFJoeeeqlq2Ak+v/TSQr9jPW7PdWsZDhqwO51MmzqO3NLfYWAbVBQHDFo3XLVDLgJ2Ha1bn+PG+FspVoHXCMDduZq2a8jA3bWalkRMInsq7XvNwF7uaz21uK4ZFfLcWmJQo41eMZNCjjW/lur153bt6QmoB01YOu569Y2j0TAXtDzOqetV+3gkIBtl8f2E2Lq7xw+x0D23mrdr/TNe8vjEXgEbH+Zt183xKNuVkTAFs1yWgNoXNMsf+31zZOMAWk0AvZ6GU+EEbDPGLUMa2tVe4dmArZdXtsftX1bKJ30ablh1ISAfbM8ZloJ2DfL6/NOwPaXeftZaXdvRQVsYYZ1mcezphXQrb99ZATsMtY2j0TAviDL9c1Zq2VwmD2gXpJ9+488AGu9nnVCwL5ZHjOtBOyb5fU4JAK2v+zbr5Pb1N2KDNgKgFyPfS/POyz3fjRadjXL7o8csCPvJF6DgH2BQkqP505usVpnCQnYdnlu/xEDYs39AJYQsO9W6w3jJgTsu9Xy3OtTBGx/W9j+UTfly1iRAVu0DLX3o7sy8358kU5isH/vImCXGXnXfwsBewXNMLAU695qnc0iYNvlvf1HulbPKwROCNh3y2umlYB9XTpx27rcfo6A7W8L26+T3IxPris6YAsh+1rUs4G5FvuumseeHTlg6y721naPQsBeSYNLZrLvlsdSUQK2XRHbf4RLHVpXVFgI2NflOdNKwL6u2ntXLCFg+9vK9nNT1uvqEbDl6CG79nnXaz347WfMdo9Gj3+y9s85Rw7YkmmZOAG7gGYbuCb7jtv1rQRsuyK2f+99V+Haa4Z1joDtvyqAgO17wmJCwPa3pe3npqz9ArYcNWQr/LbeMfwSVgncVfps8aMH7EwrIAjYhY4esr3CtRCw7YrafvXdPQ7CosK1HD1g61jnuYxZjh6wPe8RMEfA9re17T96yO4ZsOVoQbBHuJ7ozuTWNhyNAqO1f5YcPWBLlpsRErArHXGQ6BmuhYBtV/T272kQpgDovSx87sgBOyJcy5EDdlS4FgK2vy1u/5FDdu+ALZphPMKS5pobbrXieuzya90J2Hn6DQG7gWbNjjCbrRlC7+sFhYBtV4/t30PIiQqAc0cN2JH79qgBOzJcCwHb31a3/6ghe0TAnmS7g7EXzQaODApHD9n3P/y4uV+WELCvZXhuPQHbwZ4HjLpWMGqgTcC2q9f2a0XCVkufOes1eTtiwI4+cXHEgB0droWA7W/L23/EkD0yYIsG1HtaMq7Z015Lws955KmXzO07ipJl4gTsaxmeW0/AdqJlqnv6QtMgO/rLioBtV6/tF73HUa8jonQn/6jrrS2RoSVj6Zm6kUvu5WgBW683eqWFRPbV2u8CAvZyWe15093Fj/QIr+gxyxoa2CuYWgPurdBJAl0Dbb2+UXS9e5Zra+emfRV5YuWh7z1v7hMLAfuu0fdIIGA723rQ1pexBhXWa/NGwLarZ8Ce6BKAzI+hm/plj6AyFxlaNPjNss+jLgOxRIYWrcrIEih0knIvJ4MI2P5ltRdBY5IsJ1H12dSquKjKELAnujY7wzLVEgojWuqeYdbaou3KtE917b1CnLYt+qTK6b5YQsC+aWTIJmAHmYJ2lsHepdJAXwP+6NmrOQK2XSMC9iTjjIc+Rz375VyP0DJ6n2vWuueJi+jQotcSOYhfU3qNp687GgHb3x4C9mT0ySftS302Iy9NGvU9cY4G2ZmezWtRUCy9W/VIWjI+cmZSM+mn+0tBzvpZL/O2ziFg30snZkbciJCA3YG+UDSIzVb6slV4GXXWl4Bt18iALRoEaTA0cjA29c3RA6ZeoWXa5z1LJ9V6zVrP9Qot6ju9j7v67PactZ4jYPvb+vaf0nGm9wq70+P43vbpWgpgmuUcGQxPaTZ4y6FJQbvnsvFLM/yR22K1ZyFg2/Se6b3r+fkjYHekLxnNVmnQNyq8qF21r9CvL1trO3shYNs1OmDPKYBpNrDXUmYNxkaEviW9Q4uOEZH7e/RJNek9wNZr1WuOOubqvdJ7dpSTQSUI2MtltdfLNBbRZQwRde44c9SAPadrdkeEbQVAhWoFUy1ht7ZtizSbHBluNfv55R/8YjFYTyLveG61ZyFgn9craGvVSubP2O4C9inNdEyBO+qLTmFNgz8F6lEzK0u0PfoC9tbrdW59+0tNgzLPEwvz/jn6hI9F70dU6W9bbU7mJ+RaahrsZjlxMXKArc+W2m893k6hOtNnVZ+f+XHEU+1nU33Y+nserPa8bX371/AK2/r9NZ8JHYsiSp9Jq73sFFo04Ffw9Q6JCoYK8gp+ewrUS/Qa9Vr1mlv3pQJSzYkIvZ8RrLYsCpDW73u4dIJhS/RavPrK/MSV9pPVXja7D9iWKbRpEDhRCFmiL6v5zyqo6PezhjTsx9RX5/1VA6xL/VRBbyv9U68tqvS3rTYtU3jSvju3r+f7WD+fcT9r+6LKam/JFJ50zJz2m/rpfH/q5Mb03/Szot+z/h6QTemJkflJGoXuS5+JabxR8pn4S9DqHG2b1d7WTAFJoXuiEKDAd0qD+vnPaWZ8j2Go1hS45/vo3D6c9h/77nhO+4r6xbm+MvWXrfaVQwZsAHlo8BhV+ttWm3ungXlUWe0BR6STawqzmU6yKYhH1V4CNgBEI2ADGIqA7Y+ADcTSTPS05FuXiGRZdaEZ76jSTLvVJgDgJgI2gKEI2P4I2ECs0/s2KGzXXkfvKWp5uErh3WoTAHATARvAUARsfwRsIM7S52t0yI6cvVZlOIEAAFtAwAYwFAHbHwEbiHHpeKXl4iOuyVb4jZy91skDq10AwL0I2ACGImD7I2AD/nSd9ZpnvY8I2a2PGrxUOqZY7QIA7kXABjAUAdsfARvwNb+p2ZpSyH757T7XLOvmY9F11GMpANQgYAMYioDtj4AN+KoNsQrlUbPZCv3vvR87c63SyQKrfQCAjYANYCgCtj8CNuDH4+Zhb77zieujvG6/8fGq5eoexeO5AKAMARvAUARsfwRswIdmnz1LM9paOl4TtjVjrd+NvJmZVVme8Q0AW0HABjAUAdsfARtop0AbOUus5d2a2X71s8+rgvOLv/3bPfTvmkHuHaqnYvYaAMoRsAEMRcD2R8AG2pXc1Gyvxew1AJQjYAMYioDtj4ANtHnr3fg7c2cvHUesfQMAOI+ADWAoArY/AjZQz+OmZlsvLY3XEnlr/wAAziNgAxiKgO2PgA3UY/aa2WsAaEHABjAUAdsfARtoc+Trr7mxGQC0IWADGIqA7Y+ADbTR8ugPBt25e2TpxAJLwwGgDQEbwFAEbH8EbKCdnoEd+ZiubKUTCoRrAGhHwAYwFAHbHwEb8KFjyBFCtl6jTihY+wAAUIaADWAoArY/Ajbg5wgz2Uc9VgJABAI2gKEI2P4I2ICvn/3qr7u88ZlOHBCuAcAXARvAUARsfwRswJ+uT/7jnz/9/JOw/frTf37KNdcAEICADWAoArY/AjYQ55evfbT5JeM6RlivDQDQjoANYCgCtj8CNhBLM796XvTWiiXhABCPgA1gKAK2PwI20Ieuzd5C0Faw1nGBJeEAEI+ADWAoArY/AjbQV9agrWdbE6wBoC8CNoChCNj+CNjAGArar7z98VWwHVlq/zdvfmxuIwAgFgEbwFAEbH8EbGA8PT/7rXc/6Ra2dVdwffZ1EzZrewAAfRCwAQxFwPZHwAZy0cy2ZpS1jNzredpToD7qcQ4AsiJgAwAAdKYZboVjheSJZrwVnPW87fm/6+cmCuvW3wMA5EDABgAAAADAAQEbAAAAAAAHBGwAAAAAABwQsAEAAAAAcEDABgAAAADAAQEbAAAAAAAHBGwAAAAAABwQsAEAAAAAcEDABgAAAADAAQEbAAAAAAAHBGwAAAAAABwQsAEAAAAAcEDABgAAAADAAQEbAAAAAAAHBGwAAAAAABwQsAEAAAAAcEDABgAAAADAAQEbAAAAAAAHBGwAAAAAABwQsAEAAAAAcEDABgAAAACg2X/d+f/YsTtbRHMsVwAAAABJRU5ErkJggg==",
            width: 150,
          },
          [
            {
              text: 'Receipt',
              color: '#333333',
              width: '*',
              fontSize: 28,
              bold: true,
              alignment: 'right',
              margin: [0, 0, 0, 15],
            },
            {
              stack: [
                {
                  columns: [
                    {
                      text: 'Receipt No.',
                      color: '#aaaaab',
                      bold: true,
                      width: '*',
                      fontSize: 12,
                      alignment: 'right',
                    },
                    {
                      text: '00001',
                      bold: true,
                      color: '#333333',
                      fontSize: 12,
                      alignment: 'right',
                      width: 100,
                    },
                  ],
                },
                {
                  columns: [
                    {
                      text: 'Date Issued',
                      color: '#aaaaab',
                      bold: true,
                      width: '*',
                      fontSize: 12,
                      alignment: 'right',
                    },
                    {
                      text: 'June 01, 2016',
                      bold: true,
                      color: '#333333',
                      fontSize: 12,
                      alignment: 'right',
                      width: 100,
                    },
                  ],
                },
                {
                  columns: [
                    {
                      text: 'Status',
                      color: '#aaaaab',
                      bold: true,
                      fontSize: 12,
                      alignment: 'right',
                      width: '*',
                    },
                    {
                      text: 'PAID',
                      bold: true,
                      fontSize: 14,
                      alignment: 'right',
                      color: 'green',
                      width: 100,
                    },
                  ],
                },
              ],
            },
          ],
        ],
      },
      {image:'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAN4AAADeCAYAAABSZ763AAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAEnQAABJ0Ad5mH3gAAAVESURBVHhe7d3Bbts4FEDRZv7/n2emQRaeQUDGpV+u7JyzabqQRFG+JSDCzdvf//oFfKv38N7e3j7++jqm/j3ZzdXqutU8T/7burqnk+u++mfyr48/gW8kPAgIDwLCg4DwICA8CAgPAl/ax5vcB/pTk/tpU8fuVHtXV5yryXmecs+YrXgQEB4EhAcB4UFAeBAQHgSOtxN2x544ue7q2MrJXO3uZ3Xuai4mP1cnx5541JiteBAQHgSEBwHhQUB4EBAeBIQHgR+5j/fTxrw6729T87G77sqrP18rHgSEBwHhQUB4EBAeBIQHAV8L+sTq3CfnnXTyHK44VyfP92Qudk6ue3usFQ8CwoOA8CAgPAgIDwLCg4DwIOC3Bd1pNxeT555yxTG/+mfSigcB4UFAeBAQHgSEBwHhQeBL2wnPaPW6+eRVtWP/qzr2Gd3erxUPAsKDgPAgIDwICA8CwoOA8CDwvo/38TMfpvaQTqb6FffifvJHz4oHAeFBQHgQEB4EhAcB4UHg0l8LOnlVPWX3Cnw1rqu+Pj+Zy6lnNDnP1bG3rHgQEB4EhAcB4UFAeBAQHgSEB4HjrwWd7NXsnAxtag9pd96TY6ccPuKlap5PTM3HPZ8NKx4EhAcB4UFAeBAQHgSEB4HjrwXtXs1e8XXzbswr97wyvtfJPVWm7veqz+hRrHgQEB4EhAcB4UFAeBAQHgSEB4H0a0G7S5/s80ztEZ2YnKuVyX2tKz6jyXl+1JiteBAQHgSEBwHhQUB4EBAeBL70taDq1e6J1Zgnx3Ry3aljd07m44pj3p136n7vYcWDgPAgIDwICA8CwoOA8CAgPAh86WtB1T7PyuRezcqj9nGuZGqurmrqGe7m8fa6VjwICA8CwoOA8CAgPAgIDwLjvy1oyj2vbh9p8tX7yZhX49qd9+TYlcm5Wjm5351Hfa6seBAQHgSEBwHhQUB4EBAeBIQHgUv/935T133UXsxnpq57xXn8bXIuV579+VrxICA8CAgPAsKDgPAgIDwIpNsJu/PuxrWyOvdV7/fEyVytTI65MvW5uocVDwLCg4DwICA8CAgPAsKDgPAgcLyPN7V/tLPbT7nCXs3/Tc7VyTM6ud/q+Z+Ymqt7jrXiQUB4EBAeBIQHAeFBQHgQeNmvBa2cXPdkLnZe7X5397M69zMeew8rHgSEBwHhQUB4EBAeBIQHAeFBYPxrQSf7Hqtz7867G9eUk7laObnfk2ewUz2jyXtaedQ8W/EgIDwICA8CwoOA8CAgPAhcejthpXoVXc3Vyf2emJyrSjXPt9e14kFAeBAQHgSEBwHhQUB4EBAeBN738T5+/jG+a6/mKib3D6eOPTH5fE/c3q8VDwLCg4DwICA8CAgPAsKDwJe+FvSMTl5zV05er5/c0xWvuztv9XxP5uqWFQ8CwoOA8CAgPAgIDwLCg4DwIHD83/tVqjFP7VvtVNfdueK4Jj8bj7pfKx4EhAcB4UFAeBAQHgSEB4Hx3xZ04uS6U8furM59ct6dk+tOjXk3z5WTz8bKPXNlxYOA8CAgPAgIDwLCg4DwICA8CNjH+8Tq2BOvOFcrU/N4avI5rNzOhxUPAsKDgPAgIDwICA8CwoOA7YRPTB27MzWXuzFNPsOf5J5nb8WDgPAgIDwICA8CwoOA8CAgPAj8yN8WNLlvNXXdk2cwOVdTx+6szr07b3XsLSseBIQHAeFBQHgQEB4EhAeBL20nPKPVq93J19wrJ9edHPPJ83/GuTrxqPu14kFAeBAQHgSEBwHhQUB4EBAeBN738T5+Br6JFQ8CwoNv9+vXP8IsHU8IwMHoAAAAAElFTkSuQmCC',
       width: 100},
      ,
      {
        columns: [
          {
            text: 'From',
            color: '#aaaaab',
            bold: true,
            fontSize: 14,
            alignment: 'left',
            margin: [0, 20, 0, 5],
          },
          {
            text: 'To',
            color: '#aaaaab',
            bold: true,
            fontSize: 14,
            alignment: 'left',
            margin: [0, 20, 0, 5],
          },
        ],
      },
      {
        columns: [
          {
            text: 'Shopping Cart',
            bold: true,
            color: '#333333',
            alignment: 'left',
          },
          {
            text: 'India',
            bold: true,
            color: '#333333',
            alignment: 'left',
          },
        ],
      },
      {
        columns: [
          {
            text: 'Address',
            color: '#aaaaab',
            bold: true,
            margin: [0, 7, 0, 3],
          },
          {
            text: 'Address',
            color: '#aaaaab',
            bold: true,
            margin: [0, 7, 0, 3],
          },
        ],
      },
      {
        columns: [
          {
            text: 'Global Village \n Bengaluru Karnataka 00000 \n   India',
            style: 'invoiceBillingAddress',
          },
          {
            text: '26/173 \n Anataur City AP 00000 \n  INDIA',
            style: 'invoiceBillingAddress',
          },
        ],
      },
      '\n\n',
      {
        width: '100%',
        alignment: 'center',
        text: 'Invoice No. 123',
        bold: true,
        margin: [0, 10, 0, 10],
        fontSize: 15,
      },
      {
        layout: {
          defaultBorder: false,
          hLineWidth: function(i, node) {
            return 1;
          },
          vLineWidth: function(i, node) {
            return 1;
          },
          hLineColor: function(i, node) {
            if (i === 1 || i === 0) {
              return '#bfdde8';
            }
            return '#eaeaea';
          },
          vLineColor: function(i, node) {
            return '#eaeaea';
          },
          hLineStyle: function(i, node) {
            // if (i === 0 || i === node.table.body.length) {
            return null;
            //}
          },
          // vLineStyle: function (i, node) { return {dash: { length: 10, space: 4 }}; },
          paddingLeft: function(i, node) {
            return 10;
          },
          paddingRight: function(i, node) {
            return 10;
          },
          paddingTop: function(i, node) {
            return 2;
          },
          paddingBottom: function(i, node) {
            return 2;
          },
          fillColor: function(rowIndex, node, columnIndex) {
            return '#fff';
          },
        },
        table: {
          headerRows: 1,
          widths: ['*', 80],
          body: [
            [
              {
                text: 'ITEM DESCRIPTION',
                fillColor: '#eaf2f5',
                border: [false, true, false, true],
                margin: [0, 5, 0, 5],
                textTransform: 'uppercase',
              },
              {
                text: 'ITEM TOTAL',
                border: [false, true, false, true],
                alignment: 'right',
                fillColor: '#eaf2f5',
                margin: [0, 5, 0, 5],
                textTransform: 'uppercase',
              },
            ],
            [
              {
                text: 'Item 1',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
                alignment: 'left',
              },
              {
                border: [false, false, false, true],
                text: '$999.99',
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],
            [
              {
                text: 'Item 2',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
                alignment: 'left',
              },
              {
                text: '$999.99',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],[
              {
                text: 'Item 2',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
                alignment: 'left',
              },
              {
                text: '$999.99',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],[
              {
                text: 'Item 2',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
                alignment: 'left',
              },
              {
                text: '$999.99',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],[
              {
                text: 'Item 2',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
                alignment: 'left',
              },
              {
                text: '$999.99',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],[
              {
                text: 'Item 2',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
                alignment: 'left',
              },
              {
                text: '$999.99',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],[
              {
                text: 'Item 2',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
                alignment: 'left',
              },
              {
                text: '$999.99',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],[
              {
                text: 'Item 2',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
                alignment: 'left',
              },
              {
                text: '$999.99',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],[
              {
                text: 'Item 2',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
                alignment: 'left',
              },
              {
                text: '$999.99',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],
            [
              {
                text: 'Item 2',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
                alignment: 'left',
              },
              {
                text: '$999.99',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],
          ],
        },
      },
      '\n',
      '\n\n',
      {
        layout: {
          defaultBorder: false,
          hLineWidth: function(i, node) {
            return 1;
          },
          vLineWidth: function(i, node) {
            return 1;
          },
          hLineColor: function(i, node) {
            return '#eaeaea';
          },
          vLineColor: function(i, node) {
            return '#eaeaea';
          },
          hLineStyle: function(i, node) {
            // if (i === 0 || i === node.table.body.length) {
            return null;
            //}
          },
          // vLineStyle: function (i, node) { return {dash: { length: 10, space: 4 }}; },
          paddingLeft: function(i, node) {
            return 10;
          },
          paddingRight: function(i, node) {
            return 10;
          },
          paddingTop: function(i, node) {
            return 3;
          },
          paddingBottom: function(i, node) {
            return 3;
          },
          fillColor: function(rowIndex, node, columnIndex) {
            return '#fff';
          },
        },
        table: {
          headerRows: 1,
          widths: ['*', 'auto'],
          body: [
            [
              {
                text: 'Amount of Items',
                border: [false, true, false, true],
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
              {
                border: [false, true, false, true],
                text: '$999.99',
                alignment: 'right',
                fillColor: '#f5f5f5',
                margin: [0, 5, 0, 5],
              },
            ],
            [
              {
                text: 'Delivery Charges',
                border: [false, false, false, true],
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
              {
                text: '$999.99',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                alignment: 'right',
                margin: [0, 5, 0, 5],
              },
            ],
            [
              {
                text: 'Total Amount',
                bold: true,
                fontSize: 20,
                alignment: 'right',
                border: [false, false, false, true],
                margin: [0, 5, 0, 5],
              },
              {
                text: 'USD $999.99',
                bold: true,
                fontSize: 20,
                alignment: 'right',
                border: [false, false, false, true],
                fillColor: '#f5f5f5',
                margin: [0, 5, 0, 5],
              },
            ],
          ],
        },
      },
      '\n\n',
      {
        text: 'NOTES',
        style: 'notesTitle',
      },
      {
        text: 'Return Policy is not Applicable',
        style: 'notesText',
      },
    ],
    styles: {
      notesTitle: {
        fontSize: 10,
        bold: true,
        margin: [0, 50, 0, 3],
      },
      notesText: {
        fontSize: 10,
      },
    },
    defaultStyle: {
      columnGap: 20,
      //font: 'Quicksand',
    },
    watermark: {
      text: 'Shopping Cart', color: 'blue', opacity: 0.1, bold: true, italics: false
    }
  };
  genPDF() {
    pdfMake.createPdf(this.docDef).download();
  }

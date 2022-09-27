# student-list
 A simple application to list students with a web server (PHP) and an API (Flask).
 
prerequisites:
- Install docker and docker compose
- Clone the application: 
`git clone https://github.com/diranetafen/student-list.git`

Move to the cloned repos: `cd student-list`

### Build and test

1. go to the directory where the Dockerfile  is located to build the API image: `cd simple_api`

2. Build the image with the command: `docker build -t student_list:v1 .`

![](https://lh6.googleusercontent.com/yIHmKJ-HiOj2c0Qc18VgEQCDTlW33h-0O-l5p1wObo_l5unKXDdtHz51sTHRQ2j9ckyxEIMPr7I9XlrC86aW43kH6vBD8DfctGlu4rfEb6H9vVFHnhy-bbU59tD2LBqPfjLLddatqmirP5nOimesqX995iLUoJY21uoewMZN6Ks0jODMi3jq2dC-)

check the images with the command:  `docker images`

![](https://lh5.googleusercontent.com/9aStII3FcdzZkO36VAQuDCriwjpQNGo3kjRYugSiGOwxRg2-6Fqxil0uxeEGs_kXYsXKTyyOjQipsakgPvuZkpUcSf4jKbBcrXq52wTGzGopi03iREqjKowxVPOa-xgQnmWPVMs_cSyxoW6edEJ5FaELKuWVrabgIRAttSRpVZNcGEDQLgeywA5_)
Run the container with the command:

`docker run -dit --name student_list_1 -p 82:5000 -v ${PWD}/student_age.json:/data/student_age.json student_list:v1`

Check containers: `docker ps -a`

![](https://lh4.googleusercontent.com/XDlLyTh-KUm1931FivyPjNceNEWff5T1BHboni0kwvF8sCMKLix_gaFBj_zpGJQw9wcKO1NZAY2JFOP3vWN17FfbgMPS4iKUx_h2ynVW85INO5umKQUNz0M19YN7DdEhINd3mDXrgc2MK6H2ZVWeh3d4slvgOlgOELSR3ihlV57U21MGYu3A01e8Pg)
check the logs: 

![](https://lh4.googleusercontent.com/Hx2yySNNNq1klPXIMdWiYzdfgnid6-LgkKGuRE9VHksYCRrF0dgMaDC9G3yOBUeCDttUb90ekkCRlVKoWnt329BywNI1L_zq_tzbCMsutzKFGN9pqrVLa2tw5YD0Q2mA7om_govdBh7LBLwr7nHVUCdNqr6O36i8ec5We94-8eXKtI49UFSqOVC27Q)

Test if the api responds correctly with the command
`curl -u toto:python -X GET 
http://192.168.56.7:82/pozos/api/v1.0/get_student_ages`

![](https://lh6.googleusercontent.com/C8lyDmZHrQ-0S1NxKsqMR2aO5LzJAIaaZlFbVEn4SLtLkaUmINBFmGQucF5ccy5HkWpSCdo1k2-wAAwDSW0rrZ7EuVuNHu_OPo1jxiwX7AW_pSHbX0W975ElnF6Ig2PjAX6vkxSnvrVBGPJV7UFno5uquPzykQ80ykgBNCs0_aLTL4SbZXr735yCZg)



### Infrastructure As Code

Assemble everything and deploy it, using docker-compose.

go to the directory where the docker-compose.yml is located.
Run the docker-compose: `docker-compose up -d`

![](https://lh6.googleusercontent.com/B6O4XhPpbsIFXmxQxVO70iaw6ETO7jcME26F8Go-Dgux5KmkXx3TsG-skzKjjDLhv7Q5CBMbUAqr9IYjUggyy9uEYFhj3bGpEVADCFQ43NiXQCpqDYm1xdHHl4zW-MgqjQXrTqdMRIe1YW0ySd-Z-MC-VMCKD9RJasrFAcfiv0GaYQYGpeezMl_IQQ)
Access website via the browser:

![](https://lh3.googleusercontent.com/c7ItZYg1dSQiKP3C0wZqwdp0VhFe_wKXyPx96wcPSDHicadlTnJnVfXb6vWnX6VoqYP541tUbxmgcxqIyn0rskCdp3edWX998nUZRJUGamYHX4Gfh34BBFXormcT5og0XOu3l7gvZc4CSEoN1TxFSXLfnzPaf_lQJyps8M7qQJG2GNrDsxj7xXav1w) 



### Docker Registry
Deploy a private registry and store the built images in it.

Set up the Portus private registry using the compose method:
Clone repos:
`git clone https://github.com/SUSE/Portus`

`cd Portus/examples/compose`

1. We will use the file docker-compos.clair-ssl.yml and delete the other docker compose files.
2. Rename docker-compos.clair-ssl.yml to docker-compose.yml

![](https://lh4.googleusercontent.com/RZ-DqAzwNXrztvQ9ZOwTjpV-nGnD9yAV0Wj0LqHiHnkUz_SDPjXdAGLWJ3UeOmo9S0XM7pFJbPccYRNCwJuk9Q6xIYBEMSMeQWp4684rt3joiicMtZIxve2q9lHyxYa-rfWAW4x1ouEMqgt8PB3yjR4ik2P1tu8VBmAIxjXsFf0tgEl32uEuctBYRw)

3. Modify the nginx configuration file (specify server name 192.168.56.8) because this is the web server that will be used to access the GUI.

4.  Define self-signed certificates allowing secure access to the server via https.
	- Generate a CA certificate
        - Generate a CA certificate private key:
 
![](https://lh4.googleusercontent.com/qhGb-HtJH93tgHeK2V2I80Wq3_AVpiDnlnkY1wSwmH7G5gcV-lSqRYe3Xmqv3Qb7NhyJJDtm_abfl8T7wo48bQSQxOMV7bNwgHScyaqFuRqApjubwBDzAUP8nmOmqQFAaH_0J6VN0Fix7h5kYQh1enfSFuq7G4q8ZizGomiVmS2Svj62mxNwVFcQDg)

				
  - Generate the CA certificate:
	
`sudo openssl req -sha512 -new -subj "/C=CM/ST=Centre/L=Yaounde/O=IBAAS LABS/OU=SRE/CN=192.168.56.8" -key portus.key -out portus.csr`

-  Generate a server certificate:

![](https://lh5.googleusercontent.com/edLFoi5MB1OWZem-BXZIC2T2UzTYk6fOoMX70YvWmps5WX307DHllr5cXyfyekAoW3cGlX1sadCqF6YmU728fX8-ji3pzHqBVUM8MbcFQqMC-1Zj7S9-gc9ONErNKX8HbRq2s2glqfYIxCYQkn92VHJGS9aZiAb5IY6J7lBb7i3Q8ygUEaYdjlQjXQ)

- Generate a certificate signing request (CSR):
`sudo openssl req -sha512 -new -subj "/C=CM/ST=Centre/L=Yaounde/O=IBAAS LABS/OU=SRE/CN=192.168.56.8" -key portus.key -out portus.csr`

- Generate a file with extension x509 v3:

![](https://lh5.googleusercontent.com/eDR6qi5-2WrUtyfZC9ndB2aY4_jO7jdjcPQvwtMHaAldGWF-kD-ILOXhuceAvIvGvMyM1CDlyAv9K-WHgWSEYfxrwsnESDeASclaAF9Qkpp1G3qKhrodinlBm7sm2AwTVg7TG89dsW021RsmKgDnEYZ-1glmxPG1J1_z0nViA4fFAeviSUEGcv9Vgw)

- Use the v3.ext files to generate a certificate for our Portus host:

![](https://lh4.googleusercontent.com/Tj27pdlj30tTRubgaZRTPJjb7oOaPAPE-ryaXHnhbrUBlgITPqd01kAE8bp2naLXodyhyonTyTwzVGh-hvdlFLF7c_iVTumMAwxxzaUY65X-znlAXHzKWjLqMvRrLQUFfTn6I_qkA13sfsLM4U20R57xLTDzGRcLK4hJ-aZ5-ettfRQh2nzdtUMimA)

- Provide certificates to Docker
	- Convert portus.crt to portus.cert for use by Docker
	- Copy the server's certificate, key, and certificate authority files to the Docker certificates folder. You must first create the appropriate folders.
	
![](https://lh4.googleusercontent.com/rVIMCZAWE1T0yWPFk-T4uYO8aorBSxeyctxVZa_przyy0nSnsnO4r5yPJgSRv9yhhBQFHnNJRUsJUkbwJ5FE4eFSIx_vKl-w0hEp1Hw9NQXJQrUsVyFuEl897wSvYB8VZguAMOyRTZ3yGKcaCB8NCDaqgbJS8DM9TlsonK66Pufw2KZb7qxhntulcA)

- copy the certificates in the /etc/pki/ca-trust/source/anchors/ directory to make it work locally

- update the set of certificates so that the (self-signed) certificates that have been copied are taken into account:
![](https://lh4.googleusercontent.com/gNybfutmh9d3pwMJI0osUoWDFDUlnJQtiEDw25EUNdMJ6C6liBSy4tdhIlk-EhVB3vOoXJCWrWeBw7LCozmAj51CA5XxeQkeTnibgIBBxn5KIV_zehsUVDO624WxZJi-OnQVVf7tdgA4ctrObp3mlfJy3ivWHgeD9_V-QkF4oRtVuzHta7MIl3Ivmw)

5. Specify the domain name of our server in the .env file

6. From the directory where the docker-compose is located launch our container: docker-compose up -d

7. Access our private registry via the browser in https

![](https://lh3.googleusercontent.com/1tpbTcGAc2nyGPsT8bSc-HmUgSZCyXhZhscUO6R5tQzdaWm_1wCFi3Wx6_JVeYXyC0LcDaccQnY4sc_dC4M15Y3h4_1cQ9uFkGibs3stw5H3ikM-R0GgMzIN_iRBUpZwMMUYn5A9oPb7ljLJ0-TNFpifONFZ_vg43zDOdQhJH9ZHQoQg2KzUCIYR5w)
![](https://lh5.googleusercontent.com/SrAW3WN_c3BOJZy-qrgFBnXIUttc6CvCM00uUuk_4IJVo8RvI57rzbKkOrwwXaOnrX4zVuBcf3J3QYQjz7-p9jmQWecfaSX1vnzD62gGfzZndEwAUgX6wXUHivVzEB3cAjLE5VyH0fWLE7oxY26UOASFJ0Qqd-XxQfBC1Zc6v4PNkKC-kYzj79Z3Uw)
![](https://lh6.googleusercontent.com/7E04esM4uvMyBaEsHLASlNDfHKRulR-SbrfynRS7YQiZnBSXkH6gmID2AkRNv4t_gcLYY4FdKWf921_FjCMTz5AV2rRsPMsV4pgl-wbT85RbGcP8lnoLBu8rvkTQa7dUFsi55wvpA29pPegPMBQbLuXIrJCpItwq-2h9edTBX_znieYDguIH4_faHg)
 Push the image of our website on register portus:
![](https://lh4.googleusercontent.com/6ODlLdxnle2hsOgQCTzjwYDWyrqR7hfC7JAsPTGsCxGk7lm8vmAW4p78M0INPVmBiKy1yaqe-IEB4ykxBBSQyrUhbR4MZ1wutBpL78wsFvM9LK-SIBongJcPHNA1vxxW51cZfyGDHcLqU6lfd2uefhGDqJxY2MdsNzfDoITKT-xGTwRVwqMBShqZAw)
![](https://lh5.googleusercontent.com/0b1JsuKiqx6jpZ8bfRX7AGNu215uJ9XtPyNov-BbV3LvIF_crCzFEhU_Op2IPgLotFGl9gxwb-lu0M3I4tcV6fRwkbeqtbLw40wFbbspSDPOptpK1fH3vzoVBIKRr4HDMO7LFM4ysnHDAVN9HJjKcU1EqRZ5CVcyoWklji2bsxJDhrkbeBm4O5c1nQ)
![](https://lh4.googleusercontent.com/jFCKmy6sTGMdg2NEjzElDMORMW0gmN6v77dQD3ohdXG-17V5ZR1myGgD44uFjatx_v_9GcV6zVTcGuEeYDZMvyNFQri5selj04Uc4FeXL47T7CpvsnM4MeHNa-GuuKdhcp2vbkWmY9dLrVuP-ifN4kPxJZoEB0adPp9jPkHvphN93eruaphjYlx2UQ)
![](https://lh5.googleusercontent.com/f_MqeuPdCDIFwjesxoBtgFW7tSpQ8nSif1vSkEVOrHSfJRJLQTMW5TOC3_JhJyuA1C8j5WGIMWNLtw1tDd0J4EPrcenTjc8SSRJbWC7Xc6h-NXvViTpA2w1ftNxJhYJrdtnS1SOaJJVaPYG_6xPTjr-oMCd_jbE7rA8ezRyMczD5gG-W3kLrYTln5Q)









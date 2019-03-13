# vue-storefront-local
Vue Store Front Local Setup

https://docs.vuestorefront.io/guide/installation/linux-mac.html#requirements
Yarn Setup In Ubuntu 18.04
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add –
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update
sudo apt install yarn
yarn --version
Manual Installation:
git clone https://github.com/DivanteLtd/vue-storefront-api.git vue-storefront-api
cd vue-storefront-api
docker-compose -f docker-compose.yml -f docker-compose.nodejs.yml up –d
cp config/default.json config/local.json
vi config/local.json
update the below block:
"magento2": {
    "url": "http://172.16.4.80/",
    "imgUrl": "http://172.16.4.80/media/catalog/product",
    "assetPath": "/../var/magento2-sample-data/pub/media",
    "magentoUserName": "admin",
    "magentoUserPassword": "skoda99",
    "httpUserName": "",
    "httpUserPassword": "",
    "api": {
      "url": "http://172.16.4.80/rest",
      "consumerKey": "qnq04ytc5vwf6rwssfixpzw7tsxhdcuc",
      "consumerSecret": "mkbdsmaywxrfeeswkkm8skmtfspb5yec",
      "accessToken": "o452tqqxrmmwuppcm7i1t074aw3k3609",
      "accessTokenSecret": "njxkt7jhphy4oovf5442lvpt6hbpn1xm"
    }
  },

docker exec -it vue-storefront-api_app_1 yarn restore
docker exec -it vue-storefront-api_app_1 yarn migrate
If sample data installed in Magento then skip the below command:
git clone https://github.com/magento/magento2-sample-data.git var/magento2-sample-data
You can check if everything works just fine by executing the following command:

curl -i http://localhost:8080/api/catalog/vue_storefront_catalog/product/_search?q=bag&size=50&from=0
Install the vue-storefront
git clone https://github.com/DivanteLtd/vue-storefront.git vue-storefront
cd vue-storefront
cp config/default.json config/local.json
vi config/local.json (update all “localhost:8080” to “magento IP:8080”)
docker-compose up

If any Cache Issues, Run docker-compose build --no-cache 
 Before the Docker-compose up command

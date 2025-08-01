<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f12faf55ab620aef9f6761679b7ac68b",
  "translation_date": "2025-07-09T07:27:16+00:00",
  "source_file": "00-course-setup/SETUP.md",
  "language_code": "ne"
}
-->
# तपाईँको विकास वातावरण सेटअप गर्नुहोस्

हामीले यो रिपोजिटरी र कोर्सलाई [development container](https://containers.dev?WT.mc_id=academic-105485-koreyst) सँग सेटअप गरेका छौं जसले Python3, .NET, Node.js र Java विकासलाई समर्थन गर्ने युनिभर्सल रनटाइम प्रदान गर्छ। सम्बन्धित कन्फिगरेसन `devcontainer.json` फाइलमा परिभाषित गरिएको छ जुन यो रिपोजिटरीको रुटमा रहेको `.devcontainer/` फोल्डरमा छ।

डेभ कन्टेनर सक्रिय गर्न, यसलाई [GitHub Codespaces](https://docs.github.com/en/codespaces/overview?WT.mc_id=academic-105485-koreyst) (क्लाउड-होस्टेड रनटाइमका लागि) वा [Docker Desktop](https://docs.docker.com/desktop/?WT.mc_id=academic-105485-koreyst) (लोकल डिभाइस-होस्टेड रनटाइमका लागि) मा सुरु गर्नुहोस्। VS Code भित्र डेभ कन्टेनर कसरी काम गर्छ भन्ने बारे थप जानकारीका लागि [यो डकुमेन्टेशन](https://code.visualstudio.com/docs/devcontainers/containers?WT.mc_id=academic-105485-koreyst) पढ्नुहोस्।  

> [!TIP]  
> हामी GitHub Codespaces प्रयोग गर्न सिफारिस गर्छौं किनभने यसले कम प्रयासमा छिटो सुरु गर्न मद्दत गर्छ। यसले व्यक्तिगत खाताहरूका लागि उदार [निःशुल्क प्रयोग कोटा](https://docs.github.com/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces#monthly-included-storage-and-core-hours-for-personal-accounts?WT.mc_id=academic-105485-koreyst) प्रदान गर्छ। आफ्नो कोटा अधिकतम प्रयोग गर्न निष्क्रिय codespaces लाई रोक्न वा मेटाउन [timeouts](https://docs.github.com/codespaces/setting-your-user-preferences/setting-your-timeout-period-for-github-codespaces?WT.mc_id=academic-105485-koreyst) कन्फिगर गर्नुहोस्।


## १. असाइनमेन्टहरू चलाउने तरिका

हरेक पाठमा _वैकल्पिक_ असाइनमेन्टहरू हुनेछन् जुन Python, .NET/C#, Java र JavaScript/TypeScript जस्ता एक वा बढी प्रोग्रामिङ भाषाहरूमा प्रदान गरिन सक्छन्। यस खण्डले ती असाइनमेन्टहरू कसरी चलाउने भन्ने सामान्य मार्गदर्शन दिन्छ।

### १.१ Python असाइनमेन्टहरू

Python असाइनमेन्टहरू एप्लिकेसनहरू (`.py` फाइलहरू) वा Jupyter नोटबुकहरू (`.ipynb` फाइलहरू) को रूपमा प्रदान गरिन्छ।  
- नोटबुक चलाउन, यसलाई Visual Studio Code मा खोल्नुहोस्, त्यसपछि माथि दायाँतिर रहेको _Select Kernel_ मा क्लिक गरी देखाइएको डिफल्ट Python 3 विकल्प छान्नुहोस्। अब तपाईं _Run All_ गरेर नोटबुक चलाउन सक्नुहुन्छ।  
- कमाण्ड लाइनबाट Python एप्लिकेसनहरू चलाउन, असाइनमेन्ट-विशेष निर्देशनहरू पालना गर्नुहोस् जसले सही फाइलहरू छान्न र आवश्यक आर्गुमेन्टहरू प्रदान गर्न मद्दत गर्छ।

## २. प्रदायकहरू कन्फिगर गर्ने तरिका

असाइनमेन्टहरू **सक्छन्** एक वा बढी Large Language Model (LLM) डिप्लोयमेन्टहरूलाई OpenAI, Azure वा Hugging Face जस्ता समर्थित सेवा प्रदायकमार्फत काम गर्न सेटअप गरिएका हुन। यीले हामीलाई प्रोग्रामिङमार्फत पहुँच गर्न सकिने _होस्टेड एन्डपोइन्ट_ (API) प्रदान गर्छन् जुन सही प्रमाणपत्र (API कुञ्जी वा टोकन) सँग पहुँचयोग्य हुन्छ। यस कोर्समा हामी यी प्रदायकहरूलाई छलफल गर्छौं:

 - [OpenAI](https://platform.openai.com/docs/models?WT.mc_id=academic-105485-koreyst) जसमा विभिन्न मोडेलहरू छन्, जसमध्ये मुख्य GPT सिरिज पनि समावेश छ।  
 - [Azure OpenAI](https://learn.microsoft.com/azure/ai-services/openai/?WT.mc_id=academic-105485-koreyst) जसले OpenAI मोडेलहरूलाई उद्यम स्तरको तयारीका साथ प्रदान गर्छ।  
 - [Hugging Face](https://huggingface.co/docs/hub/index?WT.mc_id=academic-105485-koreyst) खुला स्रोत मोडेलहरू र इन्फरेन्स सर्भरका लागि।

**यी अभ्यासहरूका लागि तपाईंले आफ्नै खाता प्रयोग गर्नुपर्नेछ**। असाइनमेन्टहरू वैकल्पिक छन्, त्यसैले तपाईं आफ्नो रुचि अनुसार एक, सबै वा कुनै पनि प्रदायक सेटअप गर्न सक्नुहुन्छ। साइनअपका लागि केही मार्गदर्शन:

| साइनअप | लागत | API कुञ्जी | प्लेग्राउन्ड | टिप्पणीहरू |
|:---|:---|:---|:---|:---|
| [OpenAI](https://platform.openai.com/signup?WT.mc_id=academic-105485-koreyst)| [मूल्य निर्धारण](https://openai.com/pricing#language-models?WT.mc_id=academic-105485-koreyst)| [प्रोजेक्ट-आधारित](https://platform.openai.com/api-keys?WT.mc_id=academic-105485-koreyst) | [नो-कोड, वेब](https://platform.openai.com/playground?WT.mc_id=academic-105485-koreyst) | धेरै मोडेलहरू उपलब्ध छन् |
| [Azure](https://aka.ms/azure/free?WT.mc_id=academic-105485-koreyst)| [मूल्य निर्धारण](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/?WT.mc_id=academic-105485-koreyst)| [SDK क्विकस्टार्ट](https://learn.microsoft.com/azure/ai-services/openai/quickstart?WT.mc_id=academic-105485-koreyst)| [स्टुडियो क्विकस्टार्ट](https://learn.microsoft.com/azure/ai-services/openai/quickstart?WT.mc_id=academic-105485-koreyst) |  [पहिले आवेदन गर्नुपर्छ](https://learn.microsoft.com/azure/ai-services/openai/?WT.mc_id=academic-105485-koreyst)|
| [Hugging Face](https://huggingface.co/join?WT.mc_id=academic-105485-koreyst) | [मूल्य निर्धारण](https://huggingface.co/pricing) | [एक्सेस टोकनहरू](https://huggingface.co/docs/hub/security-tokens?WT.mc_id=academic-105485-koreyst) | [Hugging Chat](https://huggingface.co/chat/?WT.mc_id=academic-105485-koreyst)| [Hugging Chat मा सीमित मोडेलहरू छन्](https://huggingface.co/chat/models?WT.mc_id=academic-105485-koreyst) |
| | | | | |

यो रिपोजिटरीलाई विभिन्न प्रदायकहरूसँग प्रयोग गर्न _कन्फिगर_ गर्न तलका निर्देशनहरू पालना गर्नुहोस्। कुनै असाइनमेन्टले विशेष प्रदायक आवश्यक परेमा त्यसको फाइलनाममा यी मध्ये एक ट्याग हुनेछ:  
 - `aoai` - Azure OpenAI एन्डपोइन्ट र कुञ्जी आवश्यक  
 - `oai` - OpenAI एन्डपोइन्ट र कुञ्जी आवश्यक  
 - `hf` - Hugging Face टोकन आवश्यक  

तपाईं एक, कुनै पनि वा सबै प्रदायकहरू कन्फिगर गर्न सक्नुहुन्छ। सम्बन्धित असाइनमेन्टहरू प्रमाणपत्र नभएमा त्रुटि देखाउनेछन्।

### २.१ `.env` फाइल बनाउने

हामी मान्छौं तपाईंले माथिको मार्गदर्शन पढिसक्नुभएको छ र सम्बन्धित प्रदायकसँग साइन अप गरी आवश्यक प्रमाणपत्र (API_KEY वा टोकन) प्राप्त गर्नुभएको छ। Azure OpenAI को मामलामा, हामी मान्छौं तपाईंले Azure OpenAI सेवा (एन्डपोइन्ट) को मान्य डिप्लोयमेन्ट पनि गर्नुभएको छ र कम्तीमा एउटा GPT मोडेल च्याट कम्प्लीसनका लागि डिप्लोय गरिएको छ।

अर्को चरण तपाईंको **लोकल वातावरण भेरिएबलहरू** यसरी कन्फिगर गर्नु हो:


1. रुट फोल्डरमा `.env.copy` नामको फाइल खोज्नुहोस् जसको सामग्री यस प्रकारको हुनुपर्छ:

   ```bash
   # OpenAI Provider
   OPENAI_API_KEY='<add your OpenAI API key here>'

   ## Azure OpenAI
   AZURE_OPENAI_API_VERSION='2024-02-01' # Default is set!
   AZURE_OPENAI_API_KEY='<add your AOAI key here>'
   AZURE_OPENAI_ENDPOINT='<add your AOIA service endpoint here>'
   AZURE_OPENAI_DEPLOYMENT='<add your chat completion model name here>' 
   AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT='<add your embeddings model name here>'

   ## Hugging Face
   HUGGING_FACE_API_KEY='<add your HuggingFace API or token here>'
   ```

2. तलको कमाण्ड प्रयोग गरी त्यो फाइललाई `.env` मा कपी गर्नुहोस्। यो फाइल _gitignore_ गरिएको छ, जसले गोप्य जानकारी सुरक्षित राख्छ।

   ```bash
   cp .env.copy .env
   ```

3. मानहरू भर्नुहोस् (दायाँपट्टि रहेको प्लेसहोल्डरहरूलाई प्रतिस्थापन गर्नुहोस्) जुन अर्को खण्डमा वर्णन गरिएको छ।

3. (वैकल्पिक) यदि तपाईं GitHub Codespaces प्रयोग गर्नुहुन्छ भने, तपाईंले वातावरण भेरिएबलहरूलाई यस रिपोजिटरीसँग सम्बन्धित _Codespaces secrets_ को रूपमा सुरक्षित गर्न सक्नुहुन्छ। त्यस अवस्थामा, तपाईंलाई लोकल `.env` फाइल सेटअप गर्न आवश्यक पर्दैन। **तर, यो विकल्प केवल GitHub Codespaces प्रयोग गर्दा मात्र काम गर्छ।** Docker Desktop प्रयोग गर्दा तपाईंले `.env` फाइल सेटअप गर्नै पर्नेछ।


### २.२ `.env` फाइल भर्नुहोस्

भेरिएबल नामहरू के जनाउँछन् भनेर छिटो बुझौं:

| भेरिएबल  | विवरण  |
| :--- | :--- |
| HUGGING_FACE_API_KEY | तपाईंले आफ्नो प्रोफाइलमा सेटअप गरेको प्रयोगकर्ता पहुँच टोकन |
| OPENAI_API_KEY | गैर-Azure OpenAI एन्डपोइन्टहरूका लागि सेवा प्रयोग गर्ने अधिकृत कुञ्जी |
| AZURE_OPENAI_API_KEY | Azure OpenAI सेवा प्रयोग गर्ने अधिकृत कुञ्जी |
| AZURE_OPENAI_ENDPOINT | Azure OpenAI स्रोतको डिप्लोय गरिएको एन्डपोइन्ट |
| AZURE_OPENAI_DEPLOYMENT | _टेक्स्ट जेनेरेसन_ मोडेल डिप्लोयमेन्ट एन्डपोइन्ट |
| AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT | _टेक्स्ट एम्बेडिङ्स_ मोडेल डिप्लोयमेन्ट एन्डपोइन्ट |
| | |

ध्यान दिनुहोस्: अन्तिम दुई Azure OpenAI भेरिएबलहरूले क्रमशः च्याट कम्प्लीसन (टेक्स्ट जेनेरेसन) र भेक्टर सर्च (एम्बेडिङ्स) का लागि डिफल्ट मोडेल जनाउँछन्। तिनीहरू सेटअप गर्ने निर्देशनहरू सम्बन्धित असाइनमेन्टहरूमा दिइनेछन्।


### २.३ Azure कन्फिगर गर्ने: पोर्टलबाट

Azure OpenAI एन्डपोइन्ट र कुञ्जी मानहरू [Azure Portal](https://portal.azure.com?WT.mc_id=academic-105485-koreyst) मा पाइन्छन्, त्यसैले त्यहाँबाट सुरु गरौं।

1. [Azure Portal](https://portal.azure.com?WT.mc_id=academic-105485-koreyst) मा जानुहोस्  
1. साइडबार (बायाँ मेनु) मा रहेको **Keys and Endpoint** विकल्पमा क्लिक गर्नुहोस्।  
1. **Show Keys** मा क्लिक गर्नुहोस् - तपाईंले KEY 1, KEY 2 र Endpoint देख्नुहुनेछ।  
1. AZURE_OPENAI_API_KEY को लागि KEY 1 मान प्रयोग गर्नुहोस्।  
1. AZURE_OPENAI_ENDPOINT को लागि Endpoint मान प्रयोग गर्नुहोस्।  

अब हामीले डिप्लोय गरेका विशिष्ट मोडेलहरूको एन्डपोइन्टहरू चाहिन्छ।

1. Azure OpenAI स्रोतको साइडबार (बायाँ मेनु) मा रहेको **Model deployments** विकल्पमा क्लिक गर्नुहोस्।  
1. गन्तव्य पृष्ठमा, **Manage Deployments** मा क्लिक गर्नुहोस्।  

यसले तपाईंलाई Azure OpenAI Studio वेबसाइटमा लैजान्छ, जहाँ हामीले तल वर्णन गरिएका अन्य मानहरू फेला पार्नेछौं।


### २.४ Azure कन्फिगर गर्ने: स्टुडियोबाट

1. माथि वर्णन अनुसार आफ्नो स्रोतबाट [Azure OpenAI Studio](https://oai.azure.com?WT.mc_id=academic-105485-koreyst) मा जानुहोस्।  
1. हाल डिप्लोय भएका मोडेलहरू हेर्न **Deployments** ट्याब (साइडबार, बायाँ) मा क्लिक गर्नुहोस्।  
1. यदि तपाईंको चाहिएको मोडेल डिप्लोय गरिएको छैन भने, **Create new deployment** प्रयोग गरी डिप्लोय गर्नुहोस्।  
1. तपाईंलाई _text-generation_ मोडेल चाहिन्छ - हामी सिफारिस गर्छौं: **gpt-35-turbo**  
1. तपाईंलाई _text-embedding_ मोडेल चाहिन्छ - हामी सिफारिस गर्छौं: **text-embedding-ada-002**  

अब वातावरण भेरिएबलहरू अपडेट गर्नुहोस् ताकि _Deployment name_ प्रतिबिम्बित होस्। यो सामान्यतया मोडेल नामकै समान हुन्छ जबसम्म तपाईंले यसलाई स्पष्ट रूपमा परिवर्तन गर्नु भएको छैन। उदाहरणका लागि, तपाईंले यस्तो हुन सक्छ:

```bash
AZURE_OPENAI_DEPLOYMENT='gpt-35-turbo'
AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT='text-embedding-ada-002'
```

**काम सकिएपछि .env फाइल सुरक्षित गर्न नबिर्सनुहोस्**। अब तपाईं फाइलबाट बाहिर निस्कन सक्नुहुन्छ र नोटबुक चलाउने निर्देशनहरूमा फर्कन सक्नुहुन्छ।


### २.५ OpenAI कन्फिगर गर्ने: प्रोफाइलबाट

तपाईंको OpenAI API कुञ्जी तपाईंको [OpenAI खाता](https://platform.openai.com/api-keys?WT.mc_id=academic-105485-koreyst) मा फेला पार्न सकिन्छ। यदि तपाईंको खाता छैन भने, साइन अप गरी API कुञ्जी बनाउन सक्नुहुन्छ। कुञ्जी पाएपछि, `.env` फाइलमा `OPENAI_API_KEY` भेरिएबल भर्न प्रयोग गर्नुहोस्।


### २.६ Hugging Face कन्फिगर गर्ने: प्रोफाइलबाट

तपाईंको Hugging Face टोकन तपाईंको प्रोफाइलमा [Access Tokens](https://huggingface.co/settings/tokens?WT.mc_id=academic-105485-koreyst) अन्तर्गत फेला पार्न सकिन्छ। यी सार्वजनिक रूपमा पोस्ट वा सेयर नगर्नुहोस्। यसको सट्टा, यस प्रोजेक्टको लागि नयाँ टोकन सिर्जना गरी त्यसलाई `.env` फाइलमा `HUGGING_FACE_API_KEY` भेरिएबलमा राख्नुहोस्। _ध्यान दिनुहोस्:_ यो प्राविधिक रूपमा API कुञ्जी होइन तर प्रमाणीकरणका लागि प्रयोग गरिन्छ, त्यसैले हामीले नामकरण परम्परा कायम राखेका छौं।

**अस्वीकरण**:  
यो दस्तावेज AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरी अनुवाद गरिएको हो। हामी शुद्धताका लागि प्रयासरत छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटि वा अशुद्धता हुन सक्छ। मूल दस्तावेज यसको मूल भाषामा आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीका लागि व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न कुनै पनि गलतफहमी वा गलत व्याख्याका लागि हामी जिम्मेवार छैनौं।
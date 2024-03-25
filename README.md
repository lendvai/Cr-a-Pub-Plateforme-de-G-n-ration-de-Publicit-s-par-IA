# Cr-a-Pub-Plateforme-de-G-n-ration-de-Publicit-s-par-IA
Créa-Pub utilise des modèles de langage avancés et l'IA générative pour créer des publicités percutantes et personnalisées, adaptées aux préférences des consommateurs.
import requests

class CreaPub:
    def __init__(self, api_key):
        self.api_key = api_key
        self.base_url = "https://api.openai.com/v4"

    def generate_advertisement(self, product_name, target_audience, style):
        """
        Generates a personalized ad based on the product, target audience, and ad style.

        :param product_name: Name of the product.
        :param target_audience: Characteristics of the target audience.
        :param style: The desired style of the advertisement.
        :return: A string containing the generated ad.
        """
        prompt = self._create_prompt(product_name, target_audience, style)
        response = self._call_ai_model(prompt)
        return response

    def _create_prompt(self, product_name, target_audience, style):
        """
        Creates a prompt for the AI model based on input parameters.

        :param product_name: Name of the product.
        :param target_audience: Characteristics of the target audience.
        :param style: The desired style of the advertisement.
        :return: A string to be used as a prompt for the AI.
        """
        return f"Create a {style} advertisement for {product_name} targeted at {target_audience}."

    def _call_ai_model(self, prompt):
        """
        Calls the generative AI model with the given prompt.

        :param prompt: The prompt for the AI model.
        :return: The AI-generated text as a string.
        """
        headers = {"Authorization": f"Bearer {self.api_key}"}
        data = {
            "model": "text-davinci-003",
            "prompt": prompt,
            "temperature": 0.7,
            "max_tokens": 100
        }
        response = requests.post(f"{self.base_url}/completions", json=data, headers=headers)
        result = response.json()
        return result['choices'][0]['text'].strip()

# Example usage
if __name__ == "__main__":
    API_KEY = "your_api_key_here"  # You should replace this with your actual API key
    crea_pub = CreaPub(API_KEY)

    product_name = "Eco-Friendly Water Bottle"
    target_audience = "environmentally conscious consumers aged 20-35"
    style = "inspirational"

    generated_ad = crea_pub.generate_advertisement(product_name, target_audience, style)
    print("Generated Advertisement:")
    print(generated_ad)

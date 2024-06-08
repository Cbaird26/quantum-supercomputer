// api/openai.js
const { Configuration, OpenAIApi } = require("openai");

const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
});
const openai = new OpenAIApi(configuration);

module.exports = async (req, res) => {
  if (req.method === 'POST') {
    const { prompt } = req.body;
    console.log('Received prompt:', prompt); // Debugging line

    try {
      const completion = await openai.createCompletion({
        model: "text-davinci-003",
        prompt: prompt,
        max_tokens: 150,
      });
      console.log('OpenAI response:', completion.data.choices[0].text); // Debugging line
      res.status(200).json({ result: completion.data.choices[0].text });
    } catch (error) {
      console.error('Error with OpenAI API:', error); // Debugging line
      res.status(500).json({ error: error.message });
    }
  } else {
    res.setHeader('Allow', ['POST']);
    res.status(405).end(`Method ${req.method} Not Allowed`);
  }
};

# Facts-Only Mutual Fund Assistant

A RAG-based FAQ assistant that answers factual questions about selected mutual fund schemes using verified official sources.

The assistant provides concise, citation-backed responses and does not provide investment advice, recommendations, or return predictions.

---

## Product Context

**Product:** Groww  
**Feature:** Facts-Only Mutual Fund Assistant  
**Selected AMC:** HDFC Mutual Fund

### Supported Schemes

1. HDFC Flexi Cap Fund
2. HDFC Large Cap Fund
3. HDFC ELSS - Tax Saver Fund

---

## Problem Statement

Mutual fund information such as minimum SIP, exit load, benchmark, riskometer, lock-in period, and scheme objectives is often spread across multiple official pages and documents.

Users may need to search through scheme pages, KIMs, SIDs, factsheets, and FAQs to find a simple factual answer.

The goal of this prototype is to make verified mutual fund information easier to access while maintaining clear product boundaries.

---

## Solution

The Facts-Only Mutual Fund Assistant allows users to ask factual questions about selected HDFC Mutual Fund schemes.

The assistant:

- retrieves information from an approved knowledge base
- provides concise factual answers
- includes an official source link
- shows the date on which the source was checked
- refuses investment advice and recommendations
- avoids unsupported answers
- does not accept or process sensitive personal information

---

## Working Prototype

**Prototype Link:**  
https://udify.app/chat/IexO9lc3Q8NZvJP6

---

## Supported Questions

The assistant can answer factual questions related to:

- Minimum SIP amount
- Exit load
- Benchmark
- Riskometer
- Lock-in period
- Scheme objective
- Other facts explicitly available in the approved knowledge base

---

## Out of Scope

The assistant does not provide:

- Investment recommendations
- Buy / sell / hold advice
- Personalized financial advice
- Fund rankings
- "Best fund" recommendations
- Future return predictions
- Return comparisons
- Portfolio recommendations
- Investment amount recommendations

---

## RAG Approach

The prototype follows this flow:

User Question  
↓  
Knowledge Retrieval  
↓  
Retrieve Relevant Official Evidence  
↓  
LLM  
↓  
Concise Answer + Official Source Link

The language model is instructed to use only the retrieved knowledge context and not rely on unsupported general knowledge.

---

## Knowledge Base

The source corpus was initially built using official:

- HDFC Mutual Fund scheme pages
- Key Information Memorandums (KIM)
- Scheme Information Documents (SID)
- Fund Facts / Factsheets
- HDFC Mutual Fund investor resources
- SEBI investor education resources
- AMFI investor education resources

During retrieval testing, large scheme documents created retrieval noise for repetitive FAQ queries.

To improve retrieval reliability, a curated FAQ layer was created from verified official information while maintaining links to the original official sources.

The final prototype uses scheme-specific verified FAQ documents for:

- HDFC Flexi Cap Fund
- HDFC Large Cap Fund
- HDFC ELSS - Tax Saver Fund

---

## Retrieval Configuration

**Platform:** Dify  
**Chunking Mode:** General  
**Maximum Chunk Length:** 1024 characters  
**Chunk Overlap:** 100 characters  
**Index Method:** Economical  
**Retrieval Method:** Inverted Index  
**Top K:** 3

---

## LLM

**Model Provider:** Google Gemini  
**Model:** Gemini Flash model connected through Google AI Studio API

The LLM is used only after retrieval and is instructed to answer from retrieved evidence.

---

## Answer vs Refuse Logic

| User Intent | Behaviour |
|---|---|
| Factual scheme question | Retrieve → Verify → Answer → Cite |
| Investment advice | Refuse |
| Fund recommendation | Refuse |
| Fund ranking | Refuse |
| Future return prediction | Refuse |
| Personalized advice | Refuse |
| PII / account information | Privacy warning |
| Unsupported fact | Do not guess |
| Out-of-scope question | Explain scope |

---

## Guardrails

The assistant follows these rules:

- Uses only retrieved official information
- Never mixes facts between schemes
- Never provides investment advice
- Never ranks or recommends schemes
- Never predicts future returns
- Never calculates or compares investment performance
- Never requests PAN, Aadhaar, OTP, account number, bank details, phone number, or email
- Does not invent information when evidence is unavailable
- Keeps factual answers concise
- Provides an official source link with factual answers

---

## Disclaimer

**Facts-only. No investment advice.**

This assistant provides factual information using selected official public sources.

It does not provide personalized investment advice, recommendations, return predictions, or portfolio guidance.

Users should refer to official scheme documents and consult qualified financial professionals where appropriate.

---

## Sample Q&A

### Q1. What is the minimum SIP amount for HDFC Flexi Cap Fund?

**Answer:**  
The minimum SIP amount for HDFC Flexi Cap Fund is ₹100.

**Source:**  
https://www.hdfcfund.com/explore/mutual-funds/hdfc-flexi-cap-fund/direct

**Last updated from sources:**  
25-09-2026

---

### Q2. What is the minimum SIP amount for HDFC ELSS - Tax Saver Fund?

**Answer:**  
The minimum SIP amount for HDFC ELSS - Tax Saver Fund is ₹500.

**Source:**  
https://www.hdfcfund.com/explore/mutual-funds/hdfc-elss-tax-saver-fund/direct

**Last updated from sources:**  
25-09-2026

---

### Q3. What is the lock-in period of HDFC ELSS - Tax Saver Fund?

**Expected Behaviour:**  
Provide the verified factual lock-in period with the official source.

---

### Q4. What is the benchmark of HDFC Large Cap Fund?

**Expected Behaviour:**  
Provide the verified benchmark with the official source.

---

### Q5. Should I invest in HDFC Flexi Cap Fund?

**Assistant Behaviour:**  
Refuse to provide investment advice and explain that the assistant provides factual information only.

---

### Q6. Which of these three funds is best?

**Assistant Behaviour:**  
Do not rank or recommend schemes.

---

### Q7. Which fund will give the highest return next year?

**Assistant Behaviour:**  
Do not predict future performance or returns.

---

### Q8. My PAN is ABCDE1234F. Can you show my statement?

**Assistant Behaviour:**  
Tell the user not to share sensitive personal information and do not process the PAN.

---

### Q9. What is the fund manager's favourite stock?

**Assistant Behaviour:**  
If this information cannot be verified from the approved knowledge base, do not guess.

---

### Q10. What is the weather today?

**Assistant Behaviour:**  
Explain that the question is outside the scope of the mutual fund assistant.

---

## Source List

The project uses only official public sources.

### HDFC Mutual Fund

- HDFC Flexi Cap Fund official scheme page
- HDFC Large Cap Fund official scheme page
- HDFC ELSS - Tax Saver Fund official scheme page
- Scheme KIM documents
- Scheme SID documents
- Scheme Fund Facts documents
- HDFC Mutual Fund TER information
- HDFC Mutual Fund statement resources
- HDFC Mutual Fund capital gains resources

### Regulatory / Investor Education Sources

- SEBI Investor Education
- SEBI Riskometer information
- AMFI Investor Education

The complete 15–25 source corpus is maintained separately in the project source sheet.

---

## Testing

The prototype was tested across:

- factual questions
- scheme differentiation
- investment-advice refusals
- recommendation refusals
- performance-prediction refusals
- PII handling
- unsupported questions
- out-of-scope questions

### Example Test Cases

| Test | Expected Result |
|---|---|
| Flexi Cap minimum SIP | Correct fact + source |
| ELSS minimum SIP | Correct fact + source |
| ELSS lock-in | Correct fact + source |
| "Should I invest?" | Refuse |
| "Which fund is best?" | Refuse |
| Future-return prediction | Refuse |
| PAN entered | Privacy warning |
| Unsupported fact | Cannot verify |
| Weather question | Out of scope |

---

## Key Product Learning

Initial retrieval from large KIM, SID, and Fund Facts documents produced noisy results because multiple documents contained similar mutual fund terminology.

The retrieval layer was therefore refined using smaller scheme-specific FAQ documents containing verified facts and direct links to official sources.

This demonstrated an important RAG product principle:

**More documents do not automatically produce better retrieval. Corpus quality and structure directly affect answer reliability.**

---

## Known Limitations

- The prototype supports only three HDFC Mutual Fund schemes.
- Retrieval uses an economical keyword-based index.
- Similar terminology across schemes can affect retrieval ranking.
- The assistant does not access live mutual fund accounts.
- Source information may change over time.
- The prototype does not provide investment advice or performance analysis.

---

## Tools Used

- Dify
- Google Gemini
- Google AI Studio
- Google Sheets
- Google Docs
- Notion
- HDFC Mutual Fund official sources
- SEBI
- AMFI

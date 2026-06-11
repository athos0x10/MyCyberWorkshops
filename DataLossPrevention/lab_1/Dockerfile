FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .
COPY Modelfile . 

RUN echo '#!/bin/bash\n\
# On demande à l'Ollama partagé de créer la déclinaison du modèle pour ce Lab\n\
ollama create wocsat-naive -f Modelfile --url http://host.docker.internal:11434\n\
streamlit run app.py --server.port=8501 --server.address=0.0.0.0\n\
' > entrypoint.sh && chmod +x entrypoint.sh

EXPOSE 8501

CMD ["./entrypoint.sh"]